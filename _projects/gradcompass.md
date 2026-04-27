---
layout: page
title: gradcompass - ai-powered graduate application assistant
description: multi-agent llm system for personalized graduate school guidance and application support
img:
importance: 2
category: agentic ai & systems
related_publications: false
---

**Quick Navigation:** [Overview](#overview) • [System Architecture](#system-architecture) • [Technical Components](#technical-components) • [Key Features](#key-features) • [User Experience](#user-experience) • [Impact & Use Cases](#impact-and-use-cases) • [Future Enhancements](#future-enhancements)

---

## overview

Built a comprehensive multi-agent LLM system delivering personalized graduate school guidance, document evaluation, and recommendations through an 8-agent framework with specialized capabilities.

**Status:** Completed

## objective

Design and implement an intelligent graduate application assistant that provides:
- Personalized university recommendations
- Document evaluation and feedback (SOP, CV, essays)
- Strategic application planning and advising
- Interview preparation and simulation
- Comprehensive guidance throughout the application journey

## system architecture

### 8-Agent Framework

Each agent has a specialized role with dedicated LLM configuration:

1. **University Recommendation Agent**
   - Matches applicant profiles to suitable programs
   - Considers academic background, research interests, career goals
   - Factors in location preferences, funding, and program strengths

2. **Statement of Purpose (SOP) Evaluator**
   - Analyzes narrative structure and coherence
   - Assesses research interest articulation
   - Provides detailed improvement suggestions
   - Checks alignment with program requirements

3. **CV/Resume Reviewer**
   - Evaluates experience presentation
   - Suggests formatting improvements
   - Identifies missing or underemphasized elements
   - Tailors advice to academic standards

4. **Essay Feedback Agent**
   - Reviews supplemental essays and personal statements
   - Evaluates authenticity and voice
   - Suggests content strengthening strategies
   - Checks for common pitfalls

5. **Strategic Advising Agent**
   - Develops application timeline strategies
   - Recommends program mix (reach/target/safety)
   - Advises on application prioritization
   - Provides funding and fellowship guidance

6. **Requirements Checker**
   - Tracks program-specific requirements
   - Monitors application deadlines
   - Ensures completeness of materials
   - Flags missing components

7. **Interview Preparation Agent**
   - Generates common interview questions
   - Provides question-answering strategies
   - Offers feedback on practice responses
   - Simulates interview scenarios

8. **Interview Simulator**
   - AI-powered mock interview conductor
   - Adaptive questioning based on responses
   - Real-time feedback on answers
   - Behavioral and technical question coverage

## technical components

### RAG (Retrieval-Augmented Generation) Pipeline

**Knowledge Base:**
- University program information and requirements
- Admission statistics and trends
- Research group descriptions and faculty profiles
- Application guidelines and best practices
- Sample successful application materials

**Retrieval System:**
- Semantic search over program databases
- Context-aware document retrieval
- Dynamic knowledge injection into agent prompts
- Real-time information updates

**Integration:**
- Each agent accesses relevant knowledge subsets
- Personalized retrieval based on user profile
- Reduces hallucination through grounded responses
- Maintains factual accuracy in recommendations

### Multi-Agent Orchestration

**Agent Communication:**
- Shared context across agents for consistency
- Information passing between specialized agents
- Coordinated workflow for complex queries
- User session management

**Role-Specific LLMs:**
- Different prompting strategies per agent
- Specialized system prompts for each role
- Temperature and parameter tuning per agent
- Output format standardization

## key features

### Personalized Recommendations

**University Matching:**
- Profile-based program suggestions
- Research fit assessment
- Career goal alignment
- Financial aid considerations

**Strategic Planning:**
- Custom application timelines
- Program portfolio optimization
- Resource allocation guidance
- Deadline management

### Document Evaluation

**Comprehensive Feedback:**
- Structural analysis of application materials
- Content quality assessment
- Specific improvement recommendations
- Iterative refinement support

**Best Practice Guidance:**
- Field-specific conventions
- Program-specific tailoring
- Common mistake avoidance
- Successful example patterns

### Interview Preparation

**AI-Powered Simulation:**
- Realistic interview environment
- Adaptive question selection
- Performance feedback
- Confidence building exercises

**Question Bank:**
- Technical questions by field
- Behavioral competency questions
- Research discussion scenarios
- Program-specific inquiries

## user experience

### Workflow

1. **Profile Creation:** User inputs background, interests, goals
2. **Initial Consultation:** Strategic advising agent provides overview plan
3. **Program Discovery:** Recommendation agent suggests target programs
4. **Document Drafting:** User develops application materials with feedback
5. **Iterative Refinement:** Document evaluator agents provide multiple rounds of feedback
6. **Interview Prep:** Practice with simulator agent before real interviews
7. **Application Monitoring:** Requirements checker tracks progress and deadlines

### Interaction Modes

- **Conversational Interface:** Natural language queries and responses
- **Document Upload:** Direct material submission for evaluation
- **Guided Workflows:** Step-by-step application process support
- **On-Demand Advice:** Quick answers to specific questions

## technical implementation

**Backend:**
- Multi-agent orchestration framework
- RAG pipeline with vector database
- LLM API integration (GPT-4, Claude, etc.)
- Session and context management

**Frontend:**
- User-friendly chat interface
- Document upload and management
- Progress tracking dashboard
- Recommendation visualization

**Data Management:**
- User profile storage
- Application material versioning
- University database maintenance
- Feedback history tracking

## impact and use cases

### Target Users

- Undergraduate students planning graduate applications
- International students navigating US/UK application systems
- Career changers pursuing advanced degrees
- Researchers seeking PhD programs

### Value Proposition

**Time Savings:**
- Automated program research and filtering
- Quick document feedback cycles
- Centralized application tracking

**Quality Improvement:**
- Expert-level advice at scale
- Multiple perspective document reviews
- Data-driven recommendations

**Accessibility:**
- 24/7 availability
- Cost-effective compared to consultants
- Reduces information asymmetry

## future enhancements

**Feature Additions:**
- Integration with university application portals
- Automated letter of recommendation requests
- Post-admission decision support (offer comparison)
- Alumni network connections

**Technical Improvements:**
- Fine-tuned models for specific agent roles
- Expanded knowledge base coverage
- Multi-modal support (video interview simulation)
- Personalized learning from user feedback

**Ethical Considerations:**
- Transparency about AI limitations
- Human expert review integration
- Bias mitigation in recommendations
- Privacy protection for user data

## conclusion

GradCompass demonstrates the potential of multi-agent LLM systems to provide comprehensive, personalized support for complex, multi-stage processes like graduate school applications. By combining specialized agents with retrieval-augmented generation and intelligent orchestration, the system delivers value across the entire application journey—from initial planning through interview preparation.

---

*This project showcases how AI can democratize access to high-quality educational advising, helping students navigate complex application processes with confidence.*
