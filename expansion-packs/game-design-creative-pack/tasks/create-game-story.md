# Create Game Development Story Task

## Purpose

Create detailed, actionable game development stories that enable AI developers to implement specific game features using Flutter + Flame engine without requiring additional design decisions.

## When to Use

- Breaking down game epics into implementable stories
- Converting Game Design Documents into development tasks
- Preparing work for Flutter developers
- Ensuring clear handoffs from design to development

## Prerequisites

Before creating stories, ensure you have:

- Completed Game Design Document (GDD) or game concept
- Game Architecture Document (if available)
- Epic definition this story belongs to
- Clear understanding of the specific game feature
- Access to project's technical preferences (Flutter + Flame stack)

## Process

### 1. Story Identification

**Review Epic Context:**

- Understand the epic's overall goal
- Identify specific features that need implementation
- Review any existing stories in the epic
- Ensure no duplicate work

**Feature Analysis:**

- Reference specific GDD sections or game concept
- Understand player experience goals
- Identify technical complexity for Flutter + Flame
- Estimate implementation scope (1-3 days typical)

### 2. Story Scoping

**Single Responsibility:**

- Focus on one specific game feature or mechanic
- Ensure story is completable in 1-3 days
- Break down complex features into multiple stories
- Maintain clear boundaries with other stories

**Implementation Clarity:**

- Define exactly what needs to be built
- Specify all technical requirements for Flutter + Flame
- Include all necessary integration points
- Provide clear success criteria

### 3. Template Execution

**Load Template:**
Use `templates#game-story-tmpl` following all embedded LLM instructions

**Key Focus Areas:**

- Clear, actionable description
- Specific acceptance criteria
- Detailed technical specifications for Flutter + Flame
- Complete implementation task list
- Comprehensive testing requirements

### 4. Story Validation

**Technical Review:**

- Verify all technical specifications are complete
- Ensure integration points are clearly defined
- Confirm file paths match Flutter project structure
- Validate Dart/Flutter code patterns and classes

**Game Design Alignment:**

- Confirm story implements GDD requirements
- Verify player experience goals are met
- Check balance parameters are included
- Ensure game mechanics are correctly interpreted

**Implementation Readiness:**

- All dependencies identified
- Asset requirements specified
- Testing criteria defined
- Definition of Done complete

### 5. Quality Assurance

**Apply Checklist:**
Execute `checklists#game-story-dod-checklist` against completed story

**Story Criteria:**

- Story is immediately actionable by Flutter developer
- No design decisions left to developer
- Technical requirements are complete for Flame engine
- Testing requirements are comprehensive
- Performance requirements are specified (60 FPS target)

### 6. Story Refinement

**Developer Perspective:**

- Can a Flutter developer start implementation immediately?
- Are all technical questions answered for Flame engine?
- Is the scope appropriate for the estimated points?
- Are all dependencies clearly identified?

**Iterative Improvement:**

- Address any gaps or ambiguities
- Clarify complex technical requirements for Flutter + Flame
- Ensure story fits within epic scope
- Verify story points estimation

## Story Elements Checklist

### Required Sections

- [ ] Clear, specific description
- [ ] Complete acceptance criteria (functional, technical, game design)
- [ ] Detailed technical specifications for Flutter + Flame
- [ ] File creation/modification list
- [ ] Dart classes and component structures
- [ ] Integration point specifications
- [ ] Ordered implementation tasks
- [ ] Comprehensive testing requirements
- [ ] Performance criteria (60 FPS, mobile optimization)
- [ ] Dependencies clearly identified
- [ ] Definition of Done checklist

### Game-Specific Requirements

- [ ] GDD section references (or game concept details)
- [ ] Game mechanic implementation details for Flame
- [ ] Player experience goals
- [ ] Balance parameters
- [ ] Flutter + Flame specific requirements
- [ ] Performance targets (60 FPS, battery optimization)
- [ ] Cross-platform considerations (iOS/Android)

### Technical Quality

- [ ] Dart strict mode compliance
- [ ] Architecture document alignment
- [ ] Code organization follows Flutter standards
- [ ] Error handling requirements
- [ ] Memory management considerations for mobile
- [ ] Testing strategy defined (unit, widget, integration)

## Common Pitfalls

**Scope Issues:**

- Story too large (break into multiple stories)
- Story too vague (add specific requirements)
- Missing dependencies (identify all prerequisites)
- Unclear boundaries (define what's in/out of scope)

**Technical Issues:**

- Missing integration details for Flame components
- Incomplete technical specifications
- Undefined Dart classes or components
- Missing performance requirements for mobile

**Game Design Issues:**

- Not referencing GDD properly
- Missing player experience context
- Unclear game mechanic implementation
- Missing balance parameters

## Success Criteria

**Story Readiness:**

- [ ] Flutter developer can start implementation immediately
- [ ] No additional design decisions required
- [ ] All technical questions answered for Flame engine
- [ ] Testing strategy is complete
- [ ] Performance requirements are clear for mobile
- [ ] Story fits within epic scope

**Quality Validation:**

- [ ] Game story DOD checklist passes
- [ ] Architecture alignment confirmed
- [ ] GDD requirements covered
- [ ] Implementation tasks are ordered and specific
- [ ] Dependencies are complete and accurate

## Handoff Protocol

**To Development:**

1. Confirm story passes all DOD criteria
2. Ensure developer has access to all referenced documents
3. Verify technical specifications are clear
4. Schedule implementation start
5. Plan progress check-ins

**Documentation:**

- Mark story as "Ready for Development"
- Update epic progress tracking
- Notify relevant stakeholders
- Archive design artifacts used

## Output

The completed story should be saved as `stories/story-{id}-{feature-name}.md` and be immediately actionable by a Flutter + Flame developer, requiring no additional design input to begin implementation.
