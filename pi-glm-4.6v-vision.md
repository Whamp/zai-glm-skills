---
name: pi-glm-4.6v-vision
description: Use GLM-4.6V vision model through the pi coding agent to replicate zai-mcp-server functionality. Use for UI screenshots, OCR, error diagnosis, diagrams, data visualization, UI diff checking, general image analysis, and video analysis.
---

# PI + GLM-4.6V Vision Tools

This skill replicates the zai-mcp-server vision functionality using the `pi` coding agent with GLM-4.6V directly.

## Command Template

```bash
pi @<image_file> --provider zai --model glm-4.6v -p "<prompt>"
```

For videos:
```bash
pi @<video_file> --provider zai --model glm-4.6v -p "<prompt>"
```

## Tool 1: UI to Artifact

**Purpose:** Convert UI screenshots to code, prompts, specs, or descriptions.

### Generate Frontend Code
```bash
pi @screenshot.png --provider zai --model glm-4.6v -p "You are a frontend development expert. Analyze this UI screenshot and generate production-ready code.

First, describe in detail the layout structure, color style, main components, and interactive elements of the website in this image to facilitate subsequent code generation.

Then generate complete, responsive HTML/CSS/JavaScript code that replicates this design exactly. Include:
- Semantic HTML structure
- CSS with proper spacing, colors, typography, and responsive breakpoints
- Interactive elements with appropriate JavaScript
- Accessibility features (ARIA labels where needed)

Output the full code in a single code block."
```

### Generate AI Prompt
```bash
pi @screenshot.png --provider zai --model glm-4.6v -p "You are a UI/UX expert. Analyze this UI screenshot and create a detailed, comprehensive prompt that would allow an AI to recreate this exact design from scratch.

First, describe in detail the layout structure, color style, main components, and interactive elements of the website in this image to facilitate subsequent code generation.

Then write a prompt that includes:
1. Detailed visual description (colors, fonts, spacing, shadows, borders)
2. Layout structure (grid/flex, headers, sidebars, content areas)
3. Component breakdown (buttons, cards, forms, navigation)
4. Styling details (hover states, transitions, responsive behavior)
5. Any animations or interactive elements visible

The prompt should be detailed enough that someone could recreate this design without seeing the original."
```

### Extract Design Specification
```bash
pi @screenshot.png --provider zai --model glm-4.6v -p "You are a design system expert. Analyze this UI screenshot and extract a complete design specification.

First, describe in detail the layout structure, color style, main components, and interactive elements of the website in this image to facilitate subsequent code generation.

Then provide a structured specification including:
1. **Colors**: All colors used (primary, secondary, background, text, borders, etc.) with hex codes
2. **Typography**: Font families, sizes, weights, line heights for all text elements
3. **Spacing**: Padding, margins, gaps between elements
4. **Components**: List all UI components with their properties
5. **Layout**: Grid/flex structure, breakpoints, responsive behavior
6. **Shadows/Effects**: Box shadows, gradients, border radius values

Format as a structured design document."
```

### Generate Description
```bash
pi @screenshot.png --provider zai --model glm-4.6v -p "Describe this UI screenshot in comprehensive detail. Include:
1. Overall purpose and type of interface
2. Layout structure and organization
3. Color scheme and visual style
4. All visible components and elements
5. Typography and text hierarchy
6. Interactive elements and their likely behavior
7. Any patterns or design system usage
8. Accessibility considerations
9. Responsive design indicators
10. Overall design quality assessment"
```

---

## Tool 2: Extract Text from Screenshot (OCR)

**Purpose:** Extract text/code from screenshots with proper formatting.

### General Text Extraction
```bash
pi @screenshot.png --provider zai --model glm-4.6v -p "You are an OCR specialist. Extract ALL text from this screenshot accurately.

Requirements:
- Extract every single character of text visible in the image
- Preserve the original structure and layout
- Maintain proper indentation for code
- Keep paragraph breaks and formatting
- If there are multiple columns or sections, preserve the spatial relationship
- Include any headers, footers, labels, or small text
- For code: maintain exact syntax, indentation, and special characters

Output the extracted text in a code block for easy copying."
```

### Code Extraction (Python/JavaScript/etc)
```bash
pi @code.png --provider zai --model glm-4.6v -p "You are a code extraction expert. Extract the source code from this screenshot.

Requirements:
- Extract the complete code with 100% accuracy
- Preserve exact indentation (spaces/tabs)
- Maintain all syntax including brackets, quotes, operators
- Include any comments in the code
- Preserve the original formatting
- Do NOT add, modify, or omit any characters
- Include line numbers if visible (note them in output)

First identify the programming language. Then extract the code and output it in a code block with the proper language syntax highlighting."
```

### Multi-language Text (Chinese + English)
```bash
pi @screenshot.png --provider zai --model glm-4.6v -p "You are a multilingual OCR specialist. This image contains both Chinese and English text.

Extract ALL text from this image accurately:
- Preserve both Chinese and English characters exactly as written
- Maintain the original structure and layout
- Keep proper formatting and indentation for any code
- Preserve mixed language content
- Include all punctuation marks and special characters

Output the extracted text in a code block."
```

---

## Tool 3: Diagnose Error Screenshot

**Purpose:** Analyze error messages and provide solutions.

### Basic Error Diagnosis
```bash
pi @error.png --provider zai --model glm-4.6v -p "You are an expert debugger. Analyze this error screenshot and provide a comprehensive diagnosis.

Your analysis should include:
1. **Error Type**: What category of error is this? (syntax, runtime, dependency, network, etc.)
2. **Root Cause**: What specifically triggered this error?
3. **Error Location**: Which file, line, or component is causing the issue?
4. **Immediate Fix**: What code change or action will resolve this error?
5. **Prevention**: How can similar errors be prevented in the future?

If the error shows a stack trace, walk through the call chain and identify where it originated.

Provide specific, actionable solutions with code examples where applicable."
```

### With Context
```bash
pi @error.png --provider zai --model glm-4.6v -p "You are an expert debugger. Analyze this error screenshot with the following context:

CONTEXT: [YOUR CONTEXT HERE - e.g., 'Running Python 3.12 with Django 5.0 during database migration']

Your analysis should include:
1. **Error Type**: What category of error is this?
2. **Root Cause**: What specifically triggered this error given the context?
3. **Error Location**: Which file, line, or component is causing the issue?
4. **Immediate Fix**: What specific action will resolve this error?
5. **Prevention**: How can similar errors be prevented?

Consider the provided context when diagnosing and suggesting solutions."
```

### Stack Trace Analysis
```bash
pi @error.png --provider zai --model glm-4.6v -p "You are a stack trace analysis expert. Analyze this error screenshot which contains a stack trace.

Your analysis:
1. Trace through the complete call chain from top to bottom
2. Identify the actual origin of the error (not just where it was caught)
3. Explain what each significant frame in the trace represents
4. Highlight any relevant file paths and line numbers
5. Identify the specific operation that failed
6. Provide a direct fix for the root cause

Format your answer with the call chain breakdown and pinpoint the exact line of code that needs to change."
```

---

## Tool 4: Understand Technical Diagram

**Purpose:** Analyze architecture diagrams, flowcharts, UML, ER diagrams.

### Architecture Diagram
```bash
pi @architecture.png --provider zai --model glm-4.6v -p "You are a system architecture expert. Analyze this technical architecture diagram.

Provide a comprehensive analysis including:
1. **System Overview**: What type of system is this?
2. **Components**: List all components, services, and modules shown
3. **Connections**: How do components connect and communicate?
4. **Data Flow**: Trace the flow of data through the system
5. **Technologies**: Identify any specific technologies or patterns indicated
6. **Purpose**: Explain the purpose of each component and relationship
7. **Entry/Exit Points**: Where do requests enter and responses exit?
8. **Potential Issues**: Note any potential bottlenecks, single points of failure, or scalability concerns

Provide a clear, structured explanation that would allow someone to understand and implement this architecture."
```

### Flowchart
```bash
pi @flowchart.png --provider zai --model glm-4.6v -p "You are a flowchart analysis expert. Analyze this flowchart diagram.

Your analysis should include:
1. **Purpose**: What process or logic does this flowchart represent?
2. **Start Point**: Where does the flow begin?
3. **Decision Points**: List all decision diamonds and the conditions they check
4. **Branches**: For each decision, describe what happens on each branch
5. **End Points**: What are the possible termination states?
6. **Flow Description**: Walk through the complete flow step by step
7. **Edge Cases**: Identify any edge cases or error handling shown

Provide a clear narrative description of the complete flow."
```

### UML Diagram
```bash
pi @uml.png --provider zai --model glm-4.6v -p "You are a UML diagram expert. Analyze this UML diagram.

First, identify what type of UML diagram this is (class, sequence, activity, use case, etc.).

Then provide:
1. **Diagram Type**: Confirm the UML diagram type
2. **Elements**: List all classes, objects, actors, or other elements
3. **Relationships**: Describe all relationships (inheritance, association, dependency, etc.)
4. **Attributes/Methods**: For class diagrams, list all attributes and methods with types
5. **Interactions**: For sequence diagrams, describe the message flow
6. **Design Patterns**: Identify any design patterns evident in the diagram
7. **Implementation Notes**: What should a developer know when implementing this?

Provide a clear, structured explanation suitable for implementation."
```

### ER Diagram
```bash
pi @er-diagram.png --provider zai --model glm-4.6v -p "You are a database design expert. Analyze this Entity-Relationship diagram.

Your analysis should include:
1. **Entities**: List all entities (tables) shown
2. **Attributes**: For each entity, list all attributes with data types if shown
3. **Primary Keys**: Identify primary keys for each entity
4. **Relationships**: Describe all relationships between entities (one-to-one, one-to-many, many-to-many)
5. **Foreign Keys**: Identify foreign key relationships
6. **Cardinality**: Specify the cardinality of each relationship
7. **Constraints**: Note any constraints shown (NOT NULL, UNIQUE, etc.)
8. **SQL Schema**: Generate the CREATE TABLE statements that would implement this design

Provide both analysis and the SQL schema."
```

### General Diagram (Auto-detect)
```bash
pi @diagram.png --provider zai --model glm-4.6v -p "You are a technical diagram expert. Analyze this technical diagram.

First, identify what type of diagram this is (architecture, flowchart, UML, ER diagram, sequence diagram, state machine, etc.).

Then provide a comprehensive analysis:
1. **Diagram Type**: What type of technical diagram is this?
2. **Purpose**: What is this diagram showing or explaining?
3. **Elements**: List all elements, nodes, or components shown
4. **Relationships**: Describe connections and relationships between elements
5. **Flow/Structure**: Explain the flow or structure depicted
6. **Key Insights**: What are the key takeaways from this diagram?
7. **Implementation Notes**: What would someone need to know to implement or use this?

Provide a clear, detailed explanation."
```

---

## Tool 5: Analyze Data Visualization

**Purpose:** Extract insights from charts, graphs, dashboards.

### General Analysis
```bash
pi @chart.png --provider zai --model glm-4.6v -p "You are a data visualization expert. Analyze this chart or graph.

Your analysis should include:
1. **Chart Type**: What type of visualization is this? (bar, line, pie, scatter, etc.)
2. **Data Series**: What data series are being displayed?
3. **Axes**: What do the X and Y axes represent? Include scales and units.
4. **Trends**: What trends are visible in the data?
5. **Key Insights**: What are the 3-5 most important insights?
6. **Anomalies**: Are there any outliers, spikes, or unusual patterns?
7. **Comparisons**: If multiple data series, how do they compare?
8. **Conclusions**: What conclusions can be drawn from this visualization?

Provide specific, actionable insights with reference to the actual data values where visible."
```

### Focus on Trends
```bash
pi @chart.png --provider zai --model glm-4.6v -p "You are a data analyst specializing in trend analysis. Analyze this visualization focusing specifically on TRENDS.

Provide:
1. **Overall Trend**: Is the overall direction up, down, flat, or volatile?
2. **Rate of Change**: How fast is the data changing? Accelerating or decelerating?
3. **Patterns**: Are there cyclical patterns, seasonality, or recurring behavior?
4. **Inflection Points**: Where does the trend change direction?
5. **Comparison**: If there are multiple series, compare their trends
6. **Forecast**: Based on the trend, what is the likely near-term direction?

Be specific about time periods and magnitudes of change."
```

### Focus on Anomalies
```bash
pi @chart.png --provider zai --model glm-4.6v -p "You are a data analyst specializing in anomaly detection. Analyze this visualization focusing specifically on ANOMALIES and OUTLIERS.

Your analysis:
1. **Outliers**: Identify all data points that deviate significantly from the pattern
2. **Spikes/Drops**: Point out any sudden, dramatic changes
3. **Unusual Patterns**: Note any irregular or unexpected patterns
4. **Explanations**: For each anomaly, suggest potential causes
5. **Impact**: Assess how significant each anomaly is
6. **Investigation**: What should be investigated further?

Be specific about the values and locations of anomalies."
```

### Dashboard Analysis
```bash
pi @dashboard.png --provider zai --model glm-4.6v -p "You are a business intelligence expert. Analyze this dashboard.

Your analysis:
1. **Dashboard Purpose**: What domain or business function does this dashboard serve?
2. **Metrics**: List all KPIs and metrics shown
3. **Visualizations**: What types of charts and graphs are used?
4. **Key Insights**: What are the top 5 insights from this dashboard?
5. **Alerts**: Are there any concerning metrics or trends that need attention?
6. **Relationships**: How do different metrics relate to each other?
7. **Actions**: Based on this dashboard, what actions should be considered?

Provide actionable business insights."
```

---

## Tool 6: UI Diff Check

**Purpose:** Compare two UI screenshots for visual differences.

```bash
pi @design.png @implementation.png --provider zai --model glm-4.6v -p "You are a UI/UX QA expert specializing in visual regression testing. Compare these two UI screenshots carefully.

IMAGE 1 (Expected/Design): [first image]
IMAGE 2 (Actual/Implementation): [second image]

Your comparison should include:
1. **Overall Match**: Do the two screenshots represent the same interface? (Yes/No)

2. **Layout Differences**:
   - Alignment issues
   - Spacing inconsistencies (padding, margins, gaps)
   - Grid/column structure differences
   - Element positioning

3. **Visual Differences**:
   - Color variations (backgrounds, text, borders, accents)
   - Typography differences (fonts, sizes, weights, line heights)
   - Size/scale variations
   - Missing or extra elements

4. **Component Differences**:
   - Missing components
   - Extra components
   - Component styling differences
   - Icon differences

5. **Content Differences**:
   - Text content variations
   - Missing labels or text
   - Image/graphic differences

6. **Critical Issues**: List any differences that would be considered visual bugs

7. **Minor Issues**: List small differences that are acceptable

Format as a structured list with specific locations for each difference."
```

### Focused Comparison
```bash
pi @before.png @after.png --provider zai --model glm-4.6v -p "You are a visual comparison expert. Compare these two screenshots focusing specifically on: [YOUR FOCUS - e.g., 'navigation bar component']

Compare the images and report only on differences related to the specified focus area. Be precise about:
- Position and alignment
- Size and spacing
- Colors and styling
- Content and text
- Any visible differences in the focused area

Ignore differences in other parts of the image."
```

---

## Tool 7: General Image Analysis

**Purpose:** Analyze images that don't fit specialized categories.

```bash
pi @image.jpg --provider zai --model glm-4.6v -p "You are a visual analysis expert. Analyze this image in comprehensive detail.

Your analysis should include:
1. **Subject**: What is the primary subject of this image?
2. **Objects**: List all visible objects and elements
3. **Colors**: Describe the color palette and scheme
4. **Composition**: How is the image composed? What is the visual arrangement?
5. **Mood/Atmosphere**: What mood or feeling does the image convey?
6. **Style**: What style or aesthetic is shown?
7. **Quality**: Technical quality assessment (lighting, focus, clarity)
8. **Context**: What is the context or setting?
9. **Notable Features**: What stands out or is particularly interesting?
10. **Overall Impression**: Summary of the image

Provide a detailed, thorough description."
```

### Logo Analysis
```bash
pi @logo.png --provider zai --model glm-4.6v -p "You are a brand identity expert. Analyze this logo design.

Your analysis:
1. **Design Elements**: What shapes, symbols, or text are used?
2. **Colors**: What color scheme is used and what do they signify?
3. **Typography**: Describe any text, fonts, and typography choices
4. **Style**: What design style does this represent? (minimalist, classic, modern, playful, etc.)
5. **Scalability**: How well would this work at different sizes?
6. **Industry Appropriateness**: Does this fit its apparent industry/sector?
7. **Brand Attributes**: What brand qualities does this communicate?
8. **Strengths**: What makes this effective?
9. **Weaknesses**: Are there any potential issues?
10. **Overall Assessment**: Overall evaluation of the logo design"
```

---

## Tool 8: Analyze Video

**Purpose:** Analyze video content (MP4, MOV, M4V, max 8MB).

```bash
pi @video.mp4 --provider zai --model glm-4.6v -p "You are a video analysis expert. Analyze this video content.

Your analysis should include:
1. **Content Summary**: What is this video showing? Describe the overall content.
2. **Key Actions**: What are the main actions or events that occur?
3. **Scene Description**: Describe the setting, environment, and background
4. **Objects/Subjects**: What people, objects, or elements are featured?
5. **Movement**: Describe the motion and action sequences
6. **Progression**: How does the video progress from beginning to end?
7. **Audio**: If applicable, describe any audio or speech content
8. **Purpose**: What seems to be the purpose or context of this video?
9. **Key Moments**: Identify the most significant moments or transitions
10. **Overall Summary**: Provide a concise summary of the entire video

Provide a chronological description of what happens in the video."
```

### Tutorial/Instructional Video
```bash
pi @tutorial.mp4 --provider zai --model glm-4.6v -p "You are an educational content analyst. This appears to be a tutorial or instructional video.

Your analysis:
1. **Topic**: What topic or skill is being taught?
2. **Steps**: List each step or action demonstrated in order
3. **Key Techniques**: What techniques or methods are shown?
4. **Tools/Software**: What tools, software, or equipment are used?
5. **Verbal Instructions**: Summarize any verbal explanations given
6. **Visual Cues**: What visual aids, text, or indicators are shown?
7. **Difficulty Level**: What skill level is this appropriate for?
8. **Key Takeaways**: What are the main learning points?
9. **Complete Instructions**: Provide written instructions that someone could follow based on this video"
```

---

## Quick Reference Table

| Task | Command Pattern |
|------|-----------------|
| UI → Code | `pi @ui.png --provider zai --model glm-4.6v -p "You are a frontend development expert..."` |
| OCR Text | `pi @text.png --provider zai --model glm-4.6v -p "You are an OCR specialist..."` |
| Error Diagnosis | `pi @error.png --provider zai --model glm-4.6v -p "You are an expert debugger..."` |
| Diagram Analysis | `pi @diagram.png --provider zai --model glm-4.6v -p "You are a system architecture expert..."` |
| Chart Analysis | `pi @chart.png --provider zai --model glm-4.6v -p "You are a data visualization expert..."` |
| UI Diff | `pi @a.png @b.png --provider zai --model glm-4.6v -p "You are a UI/UX QA expert..."` |
| General Image | `pi @img.jpg --provider zai --model glm-4.6v -p "You are a visual analysis expert..."` |
| Video Analysis | `pi @video.mp4 --provider zai --model glm-4.6v -p "You are a video analysis expert..."` |

## Best Practices

1. **Use -p flag**: Always use `-p` for the prompt to ensure non-interactive output
2. **Include file with @**: Use `@filename` to attach the image/video
3. **Specify provider and model**: Always use `--provider zai --model glm-4.6v`
4. **Detailed prompts**: The prompts above are detailed for best results - don't shorten them significantly
5. **Context matters**: For error diagnosis, include programming context (language, framework)
6. **Multiple images**: For UI diff, include both images with separate `@` prefixes

## Notes

- GLM-4.6V is a 106B parameter vision model
- Video analysis may take 4-5 minutes per video
- Max video file size: 8MB
- Supported formats: PNG, JPG, JPEG for images; MP4, MOV, M4V for video
