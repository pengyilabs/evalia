# METIS — AI Exam Generation Platform

Build an AI-powered exam generation and test-taking platform in Spanish. The platform enables educators to create, manage, and deploy AI-generated assessments while students take tests with real-time AI tutoring assistance.

## Core Functionalities

### 1. Material Ingestion & Processing

- **Multi-format upload**: Accept PDF, PPT, DOC, CSV, TXT files via drag-and-drop or file picker
- **Educational platform integration**: Connect to Classroom, Moodle, Canvas, Blackboard, Teams, Google Drive to pull materials directly
- **Material library**: Store uploaded materials with metadata (filename, source, date, size), searchable and filterable by type
- **AI material analysis**: Parse uploaded documents to extract key concepts, topics, and knowledge areas for question generation

### 2. Exam Creation Workflow

- **Subject configuration**: User specifies exam subject/topic, selects experience level (Básico/Intermedio/Avanzado), and provides custom instructions
- **Material selection**: Choose which uploaded materials to use as source for question generation
- **AI generation**: System generates exam questions based on selected materials, subject, and difficulty level
- **Outline generation**: AI produces a structured outline of questions with types, options, and source citations from the material

### 3. Question Management

- **Question types**: Support three question types:
  - **Única** (Single correct answer): Multiple choice with one correct option
  - **Múltiple** (Multiple correct answers): Multiple choice with several correct options
  - **Abierta** (Open-ended): Free text response questions
- **Question editor**: Full editor for modifying generated questions:
  - Edit question text
  - Change question type
  - Modify answer options (A/B/C/D for multiple choice)
  - Set correct answers
  - Add/remove/reorder questions
  - Preview how questions appear to students
- **Question configuration**: Set point values, time limits, and other metadata per question

### 4. Exam Distribution & Sharing

- **Shareable links**: Generate unique URLs for each exam
- **QR code generation**: Create QR codes for easy mobile access
- **Social sharing**: Share exam links via WhatsApp, email
- **Exam initiation**: Direct link starts the test-taking experience

### 5. Test-Taking Experience

- **Timed exams**: Configurable countdown timer (default 25 minutes) with MM:SS display
- **Progress tracking**: Visual progress bar and question counter (e.g., "3/12")
- **Question navigation**: Previous/Next buttons, direct jump to any question via dot indicators
- **Answer input**: 
  - Multiple choice: Radio buttons (single answer) or checkboxes (multiple answers)
  - Open-ended: Text area for free response
- **Test submission**: Submit completed exam for grading

### 6. AI Study Assistant (Metis)

- **Real-time chat**: Students can ask questions about the exam content while taking the test
- **Contextual responses**: AI provides hints, explanations, and guidance without giving direct answers
- **Conversational interface**: Chat panel with message history, typing indicators
- **Voice input**: Microphone button for voice-to-text input (simulated transcription with character-by-character display)
- **Character animations**: Dynamic avatar expressions that change based on conversation context:
  - Greeting, thinking, encouraging, explaining, celebrating, listening, concerned, playful, working, neutral states
  - Automatic sprite switching based on message keywords
  - Thinking animations during AI response generation
- **Delayed greetings**: AI proactively sends encouraging messages when student navigates between questions
- **Typing indicators**: Visual feedback showing AI is processing a response

### 7. Dashboard & Analytics

- **Welcome screen**: Personalized greeting with quick access to create new exams
- **Recent evaluations**: List of recently created/used exams with metadata (date, question count, duration)
- **Quick actions**: One-click access to upload materials, generate exams, view reports
- **AI idea generation**: Option to start exam creation from scratch using AI

### 8. Reporting & Insights

- **Performance metrics**: 
  - Total evaluations created
  - Number of active students
  - Average grades across exams
  - Pass/fail rates
- **Difficulty analysis**: Breakdown of question difficulty levels (hard/medium/easy)
- **Question-level analytics**: 
  - Which questions students struggle with most
  - Success rates per question
  - AI prompt usage and effectiveness per question
- **Student performance**: Individual and aggregate test results with date ranges
- **Common mistakes**: Identification of frequently missed questions
- **AI assistant usage**: Statistics on chat sessions, messages, response times

### 9. Materials Management

- **Material library**: Centralized repository of all uploaded documents
- **Search and filter**: Find materials by name, type, date, or source
- **Bulk operations**: Select multiple materials for batch actions
- **File management**: Download, delete, and organize materials

## Data Model

### Exam
- `id`: Unique identifier
- `title`: Exam name
- `subject`: Topic/subject area
- `difficulty`: Básico / Intermedio / Avanzado
- `questions[]`: Array of question objects
- `timeLimit`: Duration in minutes
- `createdAt`: Creation timestamp
- `status`: draft / published / active / completed

### Question
- `id`: Unique identifier
- `text`: Question text
- `type`: single / multiple / open
- `options[]`: Array of answer options (for single/multiple)
- `correctAnswer[]`: Correct option ID(s)
- `points`: Point value
- `sourceMaterial`: Reference to source document
- `sourceCitation`: Quote/reference from material

### Material
- `id`: Unique identifier
- `filename`: Original filename
- `type`: pdf / ppt / doc / csv / txt
- `source`: uploaded / classroom / moodle / canvas / etc.
- `size`: File size in bytes
- `uploadedAt`: Upload timestamp
- `extractedContent`: AI-parsed content for question generation

### Student
- `id`: Unique identifier
- `name`: Student name
- `email`: Contact email
- `examsTaken[]`: Array of exam attempts
- `averageGrade`: Calculated average

### ExamAttempt
- `studentId`: Reference to student
- `examId`: Reference to exam
- `answers[]`: Student responses
- `score`: Calculated score
- `startedAt`: Start timestamp
- `completedAt`: Completion timestamp
- `chatMessages[]`: AI assistant conversation history

### ChatMessage
- `id`: Unique identifier
- `role`: student / ai
- `content`: Message text
- `timestamp`: Message time
- `context`: Current question being viewed

## Navigation & Routing

- **Hash-based routing**: `#dashboard`, `#materials`, `#reports`, `#create`, `#wizard`, `#editor`, `#fill-test`
- **Sidebar navigation**: 3 main sections — Inicio (Dashboard), Materiales (Materials), Reportes (Reports)
- **Context-dependent UI**: 
  - Main app: Sidebar + topbar visible
  - Exam creation/editor/test: Full-screen without sidebar/topbar
  - Back button returns to previous context

## AI Generation Pipeline

1. **Input processing**: Receive subject, materials, difficulty level, and custom instructions
2. **Material analysis**: Extract key concepts, definitions, and relationships from source documents
3. **Question generation**: Generate questions at specified difficulty level using extracted content
4. **Answer generation**: Create plausible distractors for multiple choice, sample answers for open-ended
5. **Validation**: Ensure questions are clear, unambiguous, and appropriately difficult
6. **Outline generation**: Present structured outline for user review and modification

## State Management

- **Page visibility**: Show/hide pages based on current route
- **Form state**: Preserve form inputs during creation workflow
- **Exam state**: Track current question, answers, timer during test-taking
- **Chat state**: Maintain message history and AI context per exam session
- **Material selection**: Track which materials are selected for generation

## Key Interactions

- `createExam()`: Initialize new exam with subject and materials
- `generateQuestions()`: Trigger AI question generation from materials
- `editQuestion(id)`: Open question editor for specific question
- `saveExam()`: Persist exam to storage
- `shareExam(id)`: Generate shareable link and QR code
- `startExam(id)`: Begin test-taking session
- `submitExam()`: Submit answers for grading
- `sendChatMessage(text)`: Send student message to AI assistant
- `getAIResponse(message)`: Generate contextual AI response
- `navigateQuestion(index)`: Jump to specific question
- `toggleTimer()` / `resetTimer()`: Control exam timer
- `filterMaterials(query, type)`: Search and filter material library
- `uploadMaterial(file)`: Process and store uploaded file
- `deleteMaterial(id)`: Remove material from library
- `getAnalytics(dateRange)`: Retrieve reporting data
- `switchPage(page)`: Navigate between sections

## Technical Architecture

- **Single-page application**: All routing handled client-side
- **Vanilla JavaScript**: No framework dependencies
- **Modular functions**: Separate functions for each major feature
- **Event-driven**: Use event listeners for user interactions
- **Local storage**: Persist data client-side (exams, materials, student progress)
- **Modular architecture**: Separate concerns — UI rendering, data management, AI integration
