name: "ZPL Label Viewer .NET WinForms Application"
description: "Create a .NET C# WinForms application to view ZPL labels using the Labelary API."

## Purpose
This PRP outlines the requirements for building a .NET C# WinForms application that allows users to enter ZPL code and view the rendered label, similar to the functionality of the Labelary.com online viewer.

## Core Principles
1.  **Context is King**: Include all necessary documentation, examples, and caveats.
2.  **Validation Loops**: Provide executable tests/builds the AI can run and fix.
3.  **Information Dense**: Use keywords and patterns from the codebase.
4.  **Progressive Success**: Start simple, validate, then enhance.
5.  **Global rules**: Be sure to follow all rules in GEMINI.md.

---

## PROJECT_SOURCE:
[Leave blank to create a new project.]

## Goal
To create a functional and user-friendly .NET C# WinForms application that replicates the core functionality of the Labelary.com ZPL viewer.

## Why
-   Provide a desktop tool for developers and label designers to quickly test and visualize ZPL code.
-   Offer a more integrated solution for users who frequently work with ZPL.

## What
A WinForms application with the following features:
-   A text editor for inputting ZPL code.
-   A viewer to display the rendered label image.
-   Controls to select label size and print density (DPI).
-   A "Render" button to trigger the label generation.
-   The application will use the Labelary API to convert ZPL to an image.

### Success Criteria
-   [ ] The application builds and runs without errors.
-   [ ] Users can enter ZPL code into a text area.
-   [ ] Users can select from common label sizes (e.g., 4x6, 2x1).
-   [ ] Users can select the print density (e.g., 8 dpmm, 12 dpmm).
-   [ ] Clicking "Render" sends the ZPL to the Labelary API and displays the returned image.
-   [ ] The application handles API errors gracefully and provides feedback to the user.

## All Needed Context

### Documentation & References
```yaml
# MUST READ - Include these in your context window
- url: https://labelary.com/service.html
  why: The primary API documentation for rendering labels.
- url: https://labelary.com/docs.html
  why: Additional ZPL commands and features.
- url: https://labelary.com/zpl.html
  why: An introduction to the ZPL language.
```

### Desired Solution/Project Structure
```bash
/ZplLabelViewer (Solution)
|--/ZplLabelViewer.Core (Class Library)
|  |--/Services
|  |  |--ILabelaryService.cs
|  |  |--LabelaryService.cs
|  |--/Models
|  |  |--LabelRequest.cs
|--/ZplLabelViewer.UI (WinForms Project)
   |--/Views
   |  |--MainForm.cs
   |--Program.cs
```

### Known Gotchas & Library Quirks
```csharp
// CRITICAL: The Labelary API is accessed via HTTP GET or POST. For long ZPL strings, POST is preferred.
// CRITICAL: Ensure proper URL encoding of ZPL code when using the GET method.
// CRITICAL: The API returns image data directly. This needs to be handled and displayed in a PictureBox.
// CRITICAL: Use async/await for API calls to keep the UI responsive.
```

## Implementation Blueprint

### Data models and structure
**ZplLabelViewer.Core/Models/LabelRequest.cs**
```csharp
public class LabelRequest
{
    public string Zpl { get; set; }
    public int Dpmm { get; set; } = 8;
    public int Width { get; set; } = 4;
    public int Height { get; set; } = 6;
}
```

### List of tasks to be completed to fulfill the PRP in the order they should be completed
```yaml
Task 1: Create Solution and Projects
  - Create a new blank solution named "ZplLabelViewer".
  - Create a .NET Class Library project named "ZplLabelViewer.Core".
  - Create a .NET Windows Forms project named "ZplLabelViewer.UI".
  - Add a project reference from ZplLabelViewer.UI to ZplLabelViewer.Core.

Task 2: Implement LabelaryService
  - In ZplLabelViewer.Core, create the ILabelaryService interface and LabelaryService class.
  - Implement a method `Task<byte[]> RenderLabelAsync(LabelRequest request)` in LabelaryService.
  - This method should make a POST request to the Labelary API endpoint: `http://api.labelary.com/v1/printers/{dpmm}/labels/{width}x{height}/0`
  - The ZPL code should be in the request body.
  - The method should return the image data as a byte array.
  - Use HttpClient for the API call.

Task 3: Design the Main Form
  - In ZplLabelViewer.UI, design the main form (MainForm.cs).
  - Add a TextBox for ZPL input (multiline).
  - Add a PictureBox to display the rendered label.
  - Add ComboBoxes for label size and DPI.
  - Add a "Render" Button.

Task 4: Implement the Main Form Logic
  - In MainForm.cs, instantiate the LabelaryService.
  - Populate the ComboBoxes with options for size (e.g., "4x6", "2x1") and DPI (e.g., "8 dpmm", "12 dpmm").
  - On "Render" button click:
    - Create a LabelRequest object from the UI controls.
    - Call the `RenderLabelAsync` method.
    - Convert the returned byte array to an Image and display it in the PictureBox.
    - Implement error handling for API calls.

Task 5: Final Touches
  - Set appropriate anchoring and docking for controls to make the form resizable.
  - Add a default ZPL example in the text box on startup.
```

## Validation Loop

### Level 1: Build & Style
```bash
# .NET specific commands
dotnet build --configuration Release
dotnet format --verify-no-changes

# Expected: No compilation errors. If errors, READ and fix.
```

### Level 2: Manual Test
1.  Run the ZplLabelViewer.UI project.
2.  Verify the main form displays correctly.
3.  Leave the default ZPL and click "Render".
4.  **Expected:** A label image appears in the PictureBox.
5.  Change the label size and DPI and click "Render".
6.  **Expected:** The label image updates with the new dimensions.
7.  Enter invalid ZPL and click "Render".
8.  **Expected:** A user-friendly error message is displayed.

## Confidence Score: 9/10
The request is straightforward and the Labelary API is simple to use. The provided structure and tasks should be sufficient for a successful implementation.
