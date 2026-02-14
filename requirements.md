# Requirements Document: AI Note Taker Chrome Extension

## Introduction

The AI Note Taker is a Chrome extension designed for the AI for Bharat hackathon that enables users to automatically generate summaries and quizzes from YouTube videos in English and major Indic languages. The system leverages Google Gemini API's video understanding capabilities to process YouTube content and provide educational tools with an "Indic-first" approach, supporting 10+ Indian languages including Hindi, Tamil, Marathi, Telugu, Bengali, Gujarati, Kannada, Malayalam, Punjabi, and Odia.

## Glossary

- **Extension**: The Chrome browser extension component that provides the user interface
- **Backend_Service**: The Node.js Express server hosted on Google Cloud Run or Firebase Cloud Function
- **Gemini_API**: Google's Gemini 2.0 Flash API with video understanding capabilities
- **YouTube_API**: YouTube Data API v3 for retrieving video metadata
- **Summary**: A condensed text representation of video content in the user's chosen language
- **Quiz**: A set of 5 multiple-choice questions generated from video content with answer keys
- **Local_Storage**: Chrome extension's local storage mechanism for persisting user data
- **Active_Tab**: The currently focused browser tab containing a YouTube video
- **Indic_Language**: Any of the major Indian languages supported by the system
- **User_Preferences**: Stored settings including language preference and theme mode
- **File_API**: The Google AI infrastructure used to temporarily store and process large media files for Gemini’s multimodal analysis.
- **Code-Switching**: The practice of alternating between two or more languages in a single conversation (e.g., "Hinglish"), common in Indian educational content.

## Requirements

### Requirement 1: YouTube Video Capture

**User Story:** As a user, I want the extension to automatically detect and capture the YouTube video I'm watching, so that I can quickly generate notes without manual URL copying.

#### Acceptance Criteria

1. WHEN a user clicks the extension icon while on a YouTube video page, THE Extension SHALL capture the active tab's URL
2. WHEN the captured URL is a valid YouTube video URL (youtube.com/watch or youtu.be format), THE Extension SHALL extract the video ID
3. IF the active tab is not a YouTube video page, THEN THE Extension SHALL display an error message indicating no YouTube video detected
4. WHEN the video URL is captured, THE Extension SHALL retrieve video metadata (title, duration, channel) using the YouTube_API
5. THE Extension SHALL validate that the video ID is non-empty before proceeding with any API calls

### Requirement 2: Multi-Language Summary Generation

**User Story:** As a user, I want to generate video summaries in my preferred Indic language, so that I can understand content in my native language.

#### Acceptance Criteria

1. WHEN a user requests a summary, THE Extension SHALL send the video URL and selected language to the Backend_Service
2. THE Backend_Service SHALL pass the YouTube URL directly to the Gemini_API as a video Part for processing
3. WHEN the Gemini_API processes the video, THE Backend_Service SHALL request a summary in the user's selected language
4. THE Extension SHALL support summary generation in at least 10 Indic languages (Hindi, Tamil, Marathi, Telugu, Bengali, Gujarati, Kannada, Malayalam, Punjabi, Odia) plus English
5. WHEN a summary is generated, THE Extension SHALL display it in the popup interface with proper Unicode rendering
6. IF the Gemini_API fails to process the video, THEN THE Backend_Service SHALL return a descriptive error message
7. WHEN generating summaries, THE Backend_Service SHALL set the default language preference to Hindi (Indic-first priority)
8. Code-Switching (Hinglish/Hybrid) Support: The system SHALL accurately process and summarize videos containing "code-switched" audio (e.g., a mix of English and Hindi/Tamil), ensuring the final summary remains entirely in the user’s selected target language.

### Requirement 3: Smart Quiz Generation

**User Story:** As a student, I want to test my understanding of the video content through automatically generated quizzes, so that I can reinforce my learning.

#### Acceptance Criteria

1. WHEN a user requests a quiz, THE Extension SHALL send the video URL to the Backend_Service with a quiz generation flag
2. THE Backend_Service SHALL instruct the Gemini_API to generate exactly 5 multiple-choice questions from the video content
3. WHEN generating quiz questions, THE Gemini_API SHALL create 4 answer options per question with exactly one correct answer
4. THE Backend_Service SHALL return quiz data including questions, options, correct answers, and explanations in the user's selected language
5. WHEN displaying the quiz, THE Extension SHALL show questions one at a time or all at once based on user preference
6. WHEN a user submits quiz answers, THE Extension SHALL calculate and display the score with correct answer feedback
7. THE Extension SHALL generate quiz questions that cover different parts of the video content (beginning, middle, end)

### Requirement 4: Local History Management

**User Story:** As a user, I want to access my previously generated summaries and quizzes, so that I can review content without regenerating it.

#### Acceptance Criteria

1. WHEN a summary or quiz is successfully generated, THE Extension SHALL store it in Local_Storage with the video ID as the key
2. THE Extension SHALL store the following data for each entry: video title, video URL, timestamp, summary text, quiz data, and selected language
3. WHEN a user opens the extension, THE Extension SHALL display a history list of previously processed videos
4. WHEN a user clicks on a history entry, THE Extension SHALL load and display the stored summary and quiz without making new API calls
5. THE Extension SHALL limit history storage to the most recent 50 entries to manage storage space
6. WHEN storage exceeds 50 entries, THE Extension SHALL remove the oldest entry automatically
7. WHEN a user requests to delete a history entry, THE Extension SHALL remove it from Local_Storage and update the display
8. THE Extension SHALL provide a "Clear All History" option that removes all stored entries after user confirmation

### Requirement 5: Theme Customization

**User Story:** As a user, I want to switch between dark and light modes, so that I can use the extension comfortably in different lighting conditions.

#### Acceptance Criteria

1. THE Extension SHALL provide a toggle control for switching between dark mode and light mode
2. WHEN a user toggles the theme, THE Extension SHALL immediately apply the new theme to all UI components
3. THE Extension SHALL persist the theme preference in Local_Storage
4. WHEN the extension is opened, THE Extension SHALL load and apply the user's saved theme preference
5. THE Extension SHALL use high-contrast colors in both themes to ensure readability
6. WHEN in dark mode, THE Extension SHALL use a dark background with light text
7. WHEN in light mode, THE Extension SHALL use a light background with dark text

### Requirement 6: Backend API Integration

**User Story:** As a developer, I want a reliable backend service that handles Gemini API communication, so that the extension can process videos securely and efficiently.

#### Acceptance Criteria

1. THE Backend_Service SHALL expose a REST API endpoint for summary generation requests
2. THE Backend_Service SHALL expose a REST API endpoint for quiz generation requests
3. WHEN receiving a request, THE Backend_Service SHALL validate the YouTube URL format before processing
4. THE Backend_Service SHALL authenticate with the Gemini_API using a secure API key stored in environment variables
5. WHEN calling the Gemini_API, The Backend_Service SHALL utilize the Google AI File API to upload video/audio content for multimodal analysis, rather than passing raw text transcripts, to ensure the AI understands visual context (on-screen text, diagrams, and demonstrations).
6. THE Backend_Service SHALL implement rate limiting to prevent API quota exhaustion
7. IF the Gemini_API returns an error, THEN THE Backend_Service SHALL log the error and return a user-friendly error message
8. THE Backend_Service SHALL set appropriate CORS headers to allow requests from the Chrome extension
9. THE Backend_Service SHALL implement request timeout handling with a maximum wait time of 60 seconds

### Requirement 7: Error Handling and User Feedback

**User Story:** As a user, I want clear feedback when something goes wrong, so that I understand what happened and what to do next.

#### Acceptance Criteria

1. WHEN any API call fails, THE Extension SHALL display a user-friendly error message in the user's selected language
2. WHEN processing a video, THE Extension SHALL display a loading indicator with progress feedback
3. IF a video is too long or unavailable, THEN THE Extension SHALL inform the user with specific error details
4. WHEN network connectivity is lost, THE Extension SHALL detect the condition and display an appropriate message
5. THE Extension SHALL provide retry functionality for failed operations
6. WHEN an error occurs, THE Extension SHALL log error details to the browser console for debugging
7. THE Extension SHALL validate user inputs (language selection, video URL) before making API calls

### Requirement 8: Performance and Optimization

**User Story:** As a user, I want the extension to work quickly and efficiently, so that I can get summaries without long wait times.

#### Acceptance Criteria

1. WHEN a user requests a summary for a previously processed video, THE Extension SHALL load it from Local_Storage within 100ms
2. THE Extension SHALL display cached video metadata immediately while fetching new summaries
3. THE Backend_Service SHALL process summary requests and return results within 30 seconds for videos under 20 minutes
4. THE Extension SHALL implement debouncing for user interactions to prevent duplicate API calls
5. WHEN multiple requests are made simultaneously, THE Backend_Service SHALL queue them appropriately
6. THE Extension SHALL minimize bundle size by code-splitting and lazy-loading components
7. THE Backend_Service SHALL implement response caching for identical requests within a 1-hour window

###Requirement 9: Data Privacy and Responsible AI

**User Story**: As a user, I want my browsing data to remain private, so that I can use the extension without worrying about being tracked.
### Acceptance Criteria

1. Zero-Tracking Policy: The Extension SHALL NOT collect or store user browsing history, cookies, or personal identifiers outside of the specific YouTube URLs explicitly processed by the user.
2. Session-Only Processing: The Backend_Service SHALL delete any temporary video/audio files from the Google Cloud storage/File API immediately after the summary or quiz is generated.
3. Safety Filtering: The system SHALL utilize Gemini’s safety settings to block the generation of summaries for videos containing hate speech or harmful content, providing a "Safety Block" notification to the user.
