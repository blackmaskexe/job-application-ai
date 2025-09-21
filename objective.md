# Cover Letter Generator - Project Objective

## Project Overview
A Next.js web application that automatically generates personalized cover letters by analyzing job descriptions against user resumes/portfolios using AI. The app focuses on solving the pain point of writing custom cover letters for each job application.

## Core Features

### 1. User Authentication & Profile
- **Authentication**: Firebase Auth with Google social login
- **User Profile**: Single resume/portfolio document storage per user
- **Document Upload**: Support PDF, DOCX, and plain text formats
- **Word Limits**: Implement word count restrictions on uploaded documents to manage API costs
- **Data Storage**: Firebase Firestore for user data, Firebase Storage for document files

### 2. Job Description Input & Validation
- **Required Fields Validation**: 
  - Company name (required)
  - Job title (required) 
  - Company type/industry (required)
- **Optional Fields**: Additional job details, requirements, responsibilities
- **Error Handling**: Warn users when optional details are missing but still allow generation
- **Input Interface**: Clean form with validation feedback

### 3. AI-Powered Cover Letter Generation
- **AI Integration**: Flexible API integration (keep options open for Claude, OpenAI, etc.)
- **Analysis Engine**: Extract key requirements/skills from job description and match against resume
- **Tone Selection**: Dropdown with predefined options (Professional, Casual, Enthusiastic, etc.)
- **Template Structure**: Classic cover letter format with proper business letter formatting

### 4. Cover Letter Customization
- **Inline Editing**: Allow users to edit generated content before export
- **Tone Adjustment**: Post-generation tone modification while preserving core content
- **Real-time Preview**: Show formatted output as user makes edits

### 5. Export & Download
- **Export Formats**: DOCX and PDF generation
- **Document Libraries**: Implement robust document generation (research best options)
- **Formatting**: Professional business letter formatting with proper spacing and alignment

### 6. Usage Management & Rate Limiting
- **Daily Limits**: 10 cover letter generations per user per day
- **Batch Processing**: Queue system for up to 3 job descriptions at once
- **Batch Cooldown**: 4-hour cooldown period after using batch feature
- **Single Generation**: Always available (within daily limits) even during batch cooldown
- **Usage Tracking**: Display remaining daily quota to users

### 7. History & Management
- **Cover Letter History**: Store previously generated cover letters
- **Company Tracking**: Keep record of companies applied to
- **Quick Access**: Easy retrieval of past cover letters for reference

## Technical Architecture

### Frontend (Next.js)
- **Framework**: Next.js 14+ with App Router
- **Styling**: Tailwind CSS
- **UI Components**: Custom components with responsive design
- **State Management**: React hooks + Context API for user state
- **Design Priority**: Desktop-first with mobile optimization

### Backend & Database
- **Authentication**: Firebase Auth
- **Database**: Firestore for user data, application history, usage tracking
- **File Storage**: Firebase Storage for resume/portfolio documents
- **API Routes**: Next.js API routes for AI integration and document processing

### AI Integration
- **Provider Flexibility**: Abstract AI provider interface for easy switching
- **Rate Limiting**: Implement request queuing and user-based limits
- **Cost Management**: Monitor and optimize API usage
- **Error Handling**: Graceful fallbacks for API failures

### Document Processing
- **Upload Handling**: File validation, size limits, format conversion
- **Text Extraction**: Parse content from PDF/DOCX for AI analysis
- **Export Generation**: DOCX/PDF creation with proper formatting

## User Flow

### Initial Setup
1. User visits site and signs in with Google
2. User uploads resume/portfolio documents
3. System validates and stores documents with word count check

### Cover Letter Generation
1. User enters job description and required details
2. System validates minimum required fields
3. User selects desired tone from dropdown
4. AI analyzes job description against user's resume
5. System generates personalized cover letter
6. User reviews and edits content inline
7. User can adjust tone post-generation
8. User exports as DOCX or PDF

### Batch Processing
1. User queues up to 3 job descriptions
2. System processes each sequentially
3. User reviews and edits each generated cover letter
4. After batch completion, user enters 4-hour cooldown
5. Single generation remains available during cooldown

## Database Schema

### Users Collection
```javascript
{
  uid: string,
  email: string,
  displayName: string,
  createdAt: timestamp,
  lastLogin: timestamp,
  dailyUsage: {
    date: string,
    count: number,
    lastBatchUsed: timestamp
  },
  documents: {
    resume: {
      fileName: string,
      storagePath: string,
      uploadedAt: timestamp,
      wordCount: number
    }
  }
}
```

### CoverLetters Collection
```javascript
{
  userId: string,
  jobTitle: string,
  companyName: string,
  companyType: string,
  jobDescription: string,
  selectedTone: string,
  generatedContent: string,
  editedContent: string,
  createdAt: timestamp,
  exported: boolean,
  exportFormat: string
}
```

## Implementation Phases

### Phase 1: Core Infrastructure
- Set up Next.js project with Tailwind CSS
- Implement Firebase Auth and Firestore integration
- Create user authentication flow
- Build document upload system

### Phase 2: AI Integration
- Implement AI provider abstraction layer
- Create job description input and validation
- Build cover letter generation engine
- Add tone selection functionality

### Phase 3: Editor & Export
- Develop inline editing interface
- Implement tone adjustment post-generation
- Add DOCX/PDF export functionality
- Create download system

### Phase 4: Usage Management
- Implement daily usage tracking
- Build batch processing queue system
- Add cooldown period management
- Create usage dashboard for users

### Phase 5: History & Polish
- Add cover letter history tracking
- Implement search and filter for past applications
- Polish UI/UX and mobile responsiveness
- Add error handling and edge cases

## Success Criteria
- Users can generate professional cover letters in under 2 minutes
- AI successfully matches user skills to job requirements
- Export formats maintain professional formatting
- Rate limiting prevents API cost overruns
- Mobile experience is fully functional
- System handles edge cases gracefully

## Technical Considerations
- Implement proper error boundaries for AI API failures
- Add loading states for all async operations
- Ensure document processing handles various file formats reliably
- Optimize for Core Web Vitals and page load speeds
- Implement proper security for file uploads and user data

## Future Enhancements (Post-V1)
- Resume tailoring feature
- Multiple resume/portfolio support
- Integration with job boards
- Advanced analytics on application success
- Team/organization accounts
- Custom cover letter templates
- AI learning from user editing patterns