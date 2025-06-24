# Story: {{Story Title}}

**Epic:** {{Epic Name}}  
**Story ID:** {{ID}}  
**Priority:** {{High|Medium|Low}}  
**Points:** {{Story Points}}  
**Status:** Draft

[[LLM: This template creates detailed game development stories that are immediately actionable by Flutter + Flame developers. Each story should focus on a single, implementable feature that contributes to the overall game functionality.

Before starting, ensure you have access to:

- Game Design Document (GDD) or game concept
- Game Architecture Document (if available)
- Any existing stories in this epic
- Technical preferences (Flutter + Flame stack)

The story should be specific enough that a developer can implement it without requiring additional design decisions.]]

## Description

[[LLM: Provide a clear, concise description of what this story implements. Focus on the specific game feature or system being built using Flutter + Flame. Reference the GDD section or game concept that defines this feature.]]

{{clear_description_of_what_needs_to_be_implemented}}

## Acceptance Criteria

[[LLM: Define specific, testable conditions that must be met for the story to be considered complete. Each criterion should be verifiable and directly related to gameplay functionality.]]

### Functional Requirements

- [ ] {{specific_functional_requirement_1}}
- [ ] {{specific_functional_requirement_2}}
- [ ] {{specific_functional_requirement_3}}

### Technical Requirements

- [ ] Code follows Dart/Flutter best practices
- [ ] Maintains 60 FPS on target mobile devices
- [ ] No memory leaks or performance degradation
- [ ] Compatible with both iOS and Android
- [ ] {{specific_technical_requirement_for_flame}}

### Game Design Requirements

- [ ] {{gameplay_requirement_from_gdd}}
- [ ] {{balance_requirement_if_applicable}}
- [ ] {{player_experience_requirement}}

## Technical Specifications

[[LLM: Provide specific technical details that guide implementation using Flutter + Flame. Include class names, file locations, and integration points based on Flutter project structure.]]

### Files to Create/Modify

**New Files:**

- `{{file_path_1}}` - {{purpose}}
- `{{file_path_2}}` - {{purpose}}

**Modified Files:**

- `{{existing_file_1}}` - {{changes_needed}}
- `{{existing_file_2}}` - {{changes_needed}}

### Class/Component Definitions

[[LLM: Define specific Dart classes and Flame components needed]]

```dart
// {{component_name}}
class {{ComponentName}} extends {{FlameComponent}} {
  {{property_1}}? {{property_name}};
  {{property_2}}? {{property_name_2}};

  @override
  Future<void> onLoad() async {
    super.onLoad();
    // Component initialization
  }

  @override
  void update(double dt) {
    super.update(dt);
    // Game logic updates
  }

  @override
  void render(Canvas canvas) {
    super.render(canvas);
    // Custom rendering if needed
  }
}

// {{game_class_name}}
class {{GameClassName}} extends {{BaseGameClass}} {
  // Game-specific properties and methods
  {{method_name}}() {
    // Implementation requirements
  }
}
```

### Integration Points

[[LLM: Specify how this feature integrates with existing Flame systems]]

**Game Integration:**

- {{game_class}}: {{integration_details}}

**Component Dependencies:**

- {{component_name}}: {{dependency_description}}

**Event Communication:**

- Emits: `{{event_name}}` when {{condition}}
- Listens: `{{event_name}}` to {{response}}

## Implementation Tasks

[[LLM: Break down the implementation into specific, ordered tasks. Each task should be completable in 1-4 hours.]]

### Dev Agent Record

**Tasks:**

- [ ] {{task_1_description}}
- [ ] {{task_2_description}}
- [ ] {{task_3_description}}
- [ ] {{task_4_description}}
- [ ] Write unit tests for {{component}}
- [ ] Widget testing for UI components
- [ ] Integration testing with {{related_system}}
- [ ] Performance testing and mobile optimization

**Debug Log:**
| Task | File | Change | Reverted? |
|------|------|--------|-----------|
| | | | |

**Completion Notes:**

<!-- Only note deviations from requirements, keep under 50 words -->

**Change Log:**

<!-- Only requirement changes during implementation -->

## Game Design Context

[[LLM: Reference the specific sections of the GDD or game concept that this story implements]]

**GDD Reference:** {{section_name}} ({{page_or_section_number}})

**Game Mechanic:** {{mechanic_name}}

**Player Experience Goal:** {{experience_description}}

**Balance Parameters:**

- {{parameter_1}}: {{value_or_range}}
- {{parameter_2}}: {{value_or_range}}

## Testing Requirements

[[LLM: Define specific testing criteria for this game feature]]

### Unit Tests

**Test Files:**

- `test/{{component_name}}_test.dart`

**Test Scenarios:**

- {{test_scenario_1}}
- {{test_scenario_2}}
- {{edge_case_test}}

### Widget Tests

**Test Files:**

- `test/widgets/{{widget_name}}_test.dart`

**UI Test Cases:**

1. {{ui_test_case_1_description}}

   - Expected: {{expected_behavior}}
   - Interactions: {{user_interactions}}

2. {{ui_test_case_2_description}}
   - Expected: {{expected_behavior}}
   - Edge Case: {{edge_case_handling}}

### Integration Tests

**Test Files:**

- `integration_test/{{feature_name}}_test.dart`

**Game Testing:**

1. {{game_test_case_1_description}}

   - Expected: {{expected_behavior}}
   - Performance: {{performance_expectation}}

2. {{game_test_case_2_description}}
   - Expected: {{expected_behavior}}
   - Mobile Performance: {{mobile_performance_requirement}}

### Performance Tests

**Metrics to Verify:**

- Frame rate maintains {{fps_target}} FPS on target devices
- Memory usage stays under {{memory_limit}}MB
- Battery impact is minimal
- {{feature_specific_performance_metric}}

## Dependencies

[[LLM: List any dependencies that must be completed before this story can be implemented]]

**Story Dependencies:**

- {{story_id}}: {{dependency_description}}

**Technical Dependencies:**

- {{flutter_package_or_component}}: {{requirement}}

**Asset Dependencies:**

- {{asset_name}}: {{asset_description_and_format}}

## Mobile Considerations

[[LLM: Specify mobile-specific requirements and optimizations]]

**Performance:**

- Target 60 FPS on mid-range devices (3+ years old)
- Memory usage optimization for limited RAM
- Battery life considerations

**Platform Differences:**

- iOS specific requirements: {{ios_requirements}}
- Android specific requirements: {{android_requirements}}

**Screen Adaptations:**

- Support for various screen sizes and aspect ratios
- Safe area handling
- Orientation support: {{portrait_landscape_both}}

## Definition of Done

- [ ] Feature implemented according to specifications
- [ ] All acceptance criteria met
- [ ] Unit tests written and passing
- [ ] Widget tests cover UI components
- [ ] Integration tests validate end-to-end functionality
- [ ] Performance requirements met on target devices
- [ ] Code reviewed and approved
- [ ] Manual testing completed on iOS and Android
- [ ] Documentation updated
- [ ] Story marked as complete in tracking system
