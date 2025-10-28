# SQL Exploder

A powerful, browser-based SQL analysis and visualization tool that 'parses' (via pattern matching) SQL files and creates interactive dependency graphs showing relationships between files, tables, stored procedures, and string literals.  built with Claude and ChatGPT and me.

## Overview

SQL Exploder helps database developers and administrators understand complex SQL codebases by visualizing dependencies and relationships across multiple SQL files. The tool processes large SQL files efficiently, extracting database objects and their relationships, then renders them as an interactive force-directed graph.

I hope you like it!  Free for personal use.  If do you like it, please consider sending a tip my way -  [![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/Q5Q51NGYZC)


## Features

### Core Functionality
- **Multi-file Analysis**: Upload and analyze multiple SQL files simultaneously
- **Large File Support**: Efficiently handles files 6MB+ using chunk-based parsing
- **Interactive Visualization**: Force-directed graph powered by D3.js
- **Drag & Drop**: Simple file upload via drag-and-drop or file selector

### Analysis Capabilities
- **Table Detection**: Identifies tables from SELECT, INSERT, UPDATE, DELETE, MERGE operations
- **Operation Tracking**: Distinguishes between READ, WRITE, and READ/WRITE operations
- **Procedure Extraction**: Captures EXEC/EXECUTE calls to stored procedures
- **String Literal Analysis**: Extracts shared string literals across files (limited to 150 per file)

### Visualization Features
- **Color-Coded Nodes**:
  - Blue: SQL Files
  - Gray: Tables
  - Orange: Procedures
  - Green: Shared String Literals
- **Color-Coded Connections**:
  - Blue: Read operations
  - Red: Write operations
  - Purple: Read & Write operations
  - Yellow: Procedure calls
  - Green: String literal usage
- **Node Filtering**: Toggle visibility of files, tables, procedures, and strings
- **Search**: Find specific nodes by name or related files
- **Interactive Details**: Click nodes to view detailed information
- **Pan & Zoom**: Navigate large graphs easily

### Performance Features
- **Async Processing**: Non-blocking file processing with progress indicators
- **Chunk-Based Parsing**: Handles large files without freezing the browser
- **Console Logging**: Detailed progress tracking in browser console

## Usage

### Getting Started

1. **Open the HTML File**: Simply open `sql-Exploder-v11.html` in a modern web browser (Chrome, Firefox, Edge, or Safari)

2. **Upload SQL Files**: 
   - Click "Choose Files" and select one or more `.sql` files
   - Or drag and drop SQL files directly onto the interface

3. **View Progress**: Watch the progress bar and status messages as files are processed

4. **Explore the Graph**:
   - Pan: Click and drag the background
   - Zoom: Use mouse wheel or pinch gesture
   - Move Nodes: Click and drag individual nodes
   - View Details: Click any node to see detailed information in the side panel

### Interface Controls

#### Header Section
- **File Upload**: Choose or drag files to analyze
- **Statistics**: View count of files, nodes, and connections
- **Search Bar**: Filter nodes by name or associated files
- **Type Toggles**: Show/hide different node types

#### Graph Canvas
- **Visual Layout**: Force-directed graph showing all relationships
- **Interactive Nodes**: Sized based on number of connections
- **Hover Tooltips**: Quick information on mouse hover

#### Details Panel (when node selected)
- **Node Information**: Name, type, and usage statistics
- **Associated Files**: List of files using this resource
- **Tables Referenced**: Tables used by SQL files (with R/W indicators)
- **Procedures Called**: Stored procedures executed
- **String Literals**: String values found in the code

## Technical Details

### Parsing Algorithm

The tool uses a multi-pass parsing strategy:

1. **Comment Removal**: Strips single-line (`--`) and multi-line (`/* */`) comments
2. **String Extraction**: Identifies string literals in single and double quotes, handling escaped quotes
3. **Table Identification**: Searches for keywords (FROM, JOIN, INSERT INTO, UPDATE, DELETE FROM, MERGE) and extracts table names
4. **Procedure Detection**: Finds EXEC/EXECUTE statements and extracts procedure names
5. **Schema Handling**: Properly handles schema-qualified names (schema.table)

### Performance Optimizations

- **Chunk Processing**: Files are processed in 100KB chunks to avoid blocking
- **Yield Points**: Regular async yields prevent UI freezing
- **String Limit**: Caps string literal extraction at 150 per file
- **Keyword Filtering**: Excludes SQL keywords from table name results
- **Progressive Rendering**: Updates UI during processing

### Graph Generation

- **Force Simulation**: Uses D3.js force-directed layout
- **Collision Detection**: Prevents node overlap
- **Dynamic Distances**: Adjusts link length based on sharing frequency
- **Charge Forces**: Configures repulsion for readable layouts

## File Format Requirements

- **File Type**: `.sql` files (text-based)
- **Encoding**: UTF-8 recommended
- **Size**: No hard limit, but 6MB+ files trigger optimized parsing
- **SQL Dialects**: Designed for MySQL/SQL Server but works with most SQL variants

## Browser Requirements

- **Modern Browser**: Chrome 90+, Firefox 88+, Edge 90+, Safari 14+
- **JavaScript**: Must be enabled
- **Required Libraries** (loaded from CDN):
  - React 18.2.0
  - React DOM 18.2.0
  - Babel Standalone
  - D3.js 7.8.5
  - Tailwind CSS

## Troubleshooting

### Files Not Processing
- Check browser console (F12) for detailed error messages
- Ensure files are valid `.sql` text files
- Try processing files one at a time to isolate issues

### Graph Not Rendering
- Verify all CDN libraries loaded successfully (check Network tab in browser dev tools)
- Refresh the page and try again
- Check console for JavaScript errors

### Performance Issues
- Large files (20MB+) may take 30-60 seconds to process
- Close other browser tabs to free memory
- Process fewer files simultaneously
- Disable string literal detection by modifying the code if not needed

### Missing Dependencies
- The tool shows relationships based on keywords; dynamic SQL or variables may not be captured
- Schema names may be inconsistent if files use different naming conventions
- Temporary tables (#temp) may not be tracked correctly

## Use Cases

### Database Documentation
Generate visual documentation of database object relationships across stored procedures and scripts.

### Impact Analysis
Identify which objects are affected by changes to a specific table or procedure.

### Code Review
Understand dependencies and data flow before making changes.

### Migration Planning
Visualize cross-file dependencies when planning schema or procedure migrations.

### Onboarding
Help new team members understand database architecture and relationships.

## Limitations

- **Static Analysis Only**: Does not execute code or connect to databases
- **Pattern Matching**: Relies on keyword detection; may miss dynamic SQL or unconventional patterns
- **String Literals**: Limited to 150 per file to avoid performance issues
- **Memory Usage**: Very large codebases (100+ files, 50MB+ total) may strain browser memory
- **SQL Dialects**: Optimized for standard SQL; dialect-specific syntax may not parse perfectly

## Technical Architecture

### Dependencies
- **React**: UI framework for component-based interface
- **D3.js**: Graph visualization and force simulation
- **Tailwind CSS**: Utility-first CSS framework
- **Babel Standalone**: JSX transformation in browser

### File Structure
Single HTML file containing:
- React components for UI
- Parsing logic in JavaScript
- D3.js visualization code
- Inline CSS via Tailwind

### Data Flow
1. User uploads files → File reader API
2. Parse each file → Extract objects
3. Build graph structure → Create nodes and links
4. Render with D3.js → Interactive visualization
5. User interaction → Filter/search/details

## Version History

### v11 (Current)
- Explosion-style branding and icon
- Optimized chunk-based parsing for large files
- Enhanced error handling and logging
- Drag-and-drop file upload
- Improved progress indicators

## Author

Created by Saul102 (Bishop)
For analyzing and documenting SQL database systems

## License

Free for personal use.  If you like it, please consider sending a tip my way -  [![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/Q5Q51NGYZC)
