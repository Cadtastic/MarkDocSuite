# MarkDocViewer Process and Sequence Flows

This document outlines the key process and sequence flows within the MarkDocViewer application, illustrating how different components interact to accomplish core tasks.

## Document Loading Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as User Interface
    participant Core as Core Engine
    participant MBK as .mbk Handler
    participant Cache as Cache Manager
    participant RE as Render Engine
    participant TE as Tab Engine
    
    User->>UI: Open .mbk file
    UI->>Core: Open file request
    
    alt File in Cache
        Core->>Cache: Check cache
        Cache-->>Core: Cached content
    else File Not Cached
        Core->>MBK: Parse file
        MBK->>MBK: Extract metadata
        MBK->>MBK: Validate structure
        MBK->>MBK: Extract content
        MBK->>MBK: Process assets
        MBK-->>Core: Document content
        Core->>Cache: Store in cache
        Cache-->>Core: Cache confirmation
    end
    
    Core->>RE: Initialize renderer
    RE->>RE: Process markdown
    RE->>RE: Prepare visual elements
    RE-->>Core: Render ready
    
    Core->>TE: Create new tab
    TE->>TE: Set up tab state
    TE->>TE: Add to tab history
    TE-->>Core: Tab created
    
    Core->>UI: Update interface
    UI-->>User: Display document
    
    Core->>Core: Track reading position
    Core->>Core: Update recent documents
```

## Navigation Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as User Interface
    participant Core as Core Engine
    participant TOC as Table of Contents
    participant RE as Render Engine
    participant History as Navigation History
    
    User->>UI: Click on TOC item
    UI->>Core: Navigation request
    Core->>TOC: Get target location
    TOC-->>Core: Section identifier
    
    Core->>History: Record current position
    History-->>Core: Position saved
    
    Core->>RE: Scroll to section
    RE->>RE: Calculate position
    RE->>RE: Apply smooth scrolling
    RE-->>Core: Navigation complete
    
    Core->>UI: Update UI state
    UI->>UI: Update breadcrumb
    UI->>UI: Highlight current TOC item
    UI-->>User: Document scrolled to section
    
    alt User Goes Back
        User->>UI: Click back button
        UI->>Core: Back navigation request
        Core->>History: Get previous position
        History-->>Core: Previous location
        Core->>RE: Scroll to previous position
        RE-->>Core: Navigation complete
        Core->>UI: Update UI state
        UI-->>User: Document returned to previous position
    end
```

## Tab Management Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as User Interface
    participant Core as Core Engine
    participant TE as Tab Engine
    participant State as State Manager
    
    User->>UI: Open multiple documents
    
    loop For each document
        UI->>Core: Open document request
        Core->>TE: Create tab
        TE->>TE: Generate tab ID
        TE->>TE: Set up tab state
        TE-->>Core: Tab created
        Core->>UI: Update tab bar
        UI-->>User: Show new tab
    end
    
    User->>UI: Switch between tabs
    UI->>Core: Tab switch request
    Core->>TE: Activate tab
    TE->>TE: Update active tab
    TE->>TE: Record tab history
    TE-->>Core: Tab activated
    Core->>UI: Display tab content
    UI-->>User: Show selected document
    
    User->>UI: Reorder tabs
    UI->>Core: Tab order change
    Core->>TE: Update tab order
    TE->>TE: Reorganize tabs
    TE-->>Core: Order updated
    Core->>UI: Update tab display
    UI-->>User: Show reordered tabs
    
    User->>UI: Close tab
    UI->>Core: Close tab request
    
    alt Unsaved Changes
        Core->>UI: Prompt for confirmation
        UI-->>User: Show confirmation dialog
        User->>UI: Confirm close
        UI->>Core: Confirmation
    end
    
    Core->>TE: Close tab
    TE->>TE: Clean up resources
    TE->>TE: Update tab list
    TE-->>Core: Tab closed
    Core->>State: Save session state
    State-->>Core: State saved
    Core->>UI: Update interface
    UI-->>User: Tab removed
```

## Project Management Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as User Interface
    participant Core as Core Engine
    participant PM as Project Manager
    participant MDP as .mdproj Handler
    participant TE as Tab Engine
    
    User->>UI: Open project
    UI->>Core: Open project request
    Core->>MDP: Load project file
    MDP->>MDP: Parse project structure
    MDP->>MDP: Validate references
    MDP->>MDP: Extract metadata
    MDP-->>Core: Project data
    
    Core->>PM: Initialize project
    PM->>PM: Set up project structure
    PM-->>Core: Project initialized
    
    Core->>TE: Configure tabs
    
    loop For each document in project
        Core->>Core: Open document
        Note right of Core: See Document Loading Flow
    end
    
    Core->>UI: Update project view
    UI-->>User: Show project structure
    
    User->>UI: Navigate within project
    UI->>Core: Project navigation request
    Core->>PM: Get document reference
    PM-->>Core: Document identifier
    Core->>TE: Activate document tab
    TE-->>Core: Tab activated
    Core->>UI: Update interface
    UI-->>User: Show selected document
    
    User->>UI: Save project state
    UI->>Core: Save project request
    Core->>PM: Prepare project data
    PM->>PM: Collect tab states
    PM->>PM: Update metadata
    PM-->>Core: Updated project data
    Core->>MDP: Save project file
    MDP-->>Core: Save confirmation
    Core->>UI: Show confirmation
    UI-->>User: Project saved notification
```

## Search Process Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as User Interface
    participant Core as Core Engine
    participant SE as Search Engine
    participant Idx as Search Index
    participant RE as Render Engine
    
    User->>UI: Enter search query
    UI->>Core: Search request
    
    alt Index Exists
        Core->>Idx: Query index
    else Create Index
        Core->>SE: Create search index
        SE->>SE: Process document content
        SE->>SE: Build index
        SE->>Idx: Store index
        Idx-->>Core: Index ready
        Core->>Idx: Query index
    end
    
    Idx->>Idx: Execute query
    Idx->>Idx: Rank results
    Idx-->>Core: Search results
    
    Core->>UI: Display results
    UI-->>User: Show search results
    
    User->>UI: Select search result
    UI->>Core: Navigate to result
    Core->>RE: Scroll to location
    RE->>RE: Highlight match
    RE-->>Core: Location in view
    Core->>UI: Update display
    UI-->>User: Show document at match location
    
    User->>UI: Navigate between results
    UI->>Core: Next/previous result
    Core->>SE: Get next/previous match
    SE-->>Core: Match location
    Core->>RE: Scroll to location
    RE->>RE: Highlight match
    RE-->>Core: Location in view
    Core->>UI: Update display
    UI-->>User: Show next/previous match
```

## Annotation Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as User Interface
    participant Core as Core Engine
    participant AM as Annotation Manager
    participant RE as Render Engine
    participant Store as Annotation Storage
    
    User->>UI: Select text
    UI->>Core: Selection event
    Core->>UI: Show annotation tools
    UI-->>User: Display annotation options
    
    User->>UI: Create highlight
    UI->>Core: Highlight request
    Core->>AM: Create highlight
    AM->>AM: Generate annotation ID
    AM->>AM: Store selection range
    AM->>AM: Assign properties
    AM-->>Core: Highlight created
    
    Core->>RE: Apply highlight
    RE->>RE: Render highlight
    RE-->>Core: Visual update complete
    
    Core->>Store: Save annotation
    Store-->>Core: Save confirmation
    
    Core->>UI: Update interface
    UI-->>User: Show highlighted text
    
    Note over User, Store: Later interactions
    
    User->>UI: View annotations
    UI->>Core: List annotations request
    Core->>AM: Get annotations
    AM->>Store: Retrieve annotations
    Store-->>AM: Stored annotations
    AM-->>Core: Annotation list
    Core->>UI: Display annotations
    UI-->>User: Show annotation list
    
    User->>UI: Select annotation from list
    UI->>Core: Navigate to annotation
    Core->>AM: Get annotation location
    AM-->>Core: Location data
    Core->>RE: Scroll to location
    RE-->>Core: Location in view
    Core->>UI: Update display
    UI-->>User: Show document at annotation
```

## Theme Change Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as User Interface
    participant Core as Core Engine
    participant TM as Theme Manager
    participant RE as Render Engine
    participant Store as Settings Storage
    
    User->>UI: Change theme
    UI->>Core: Theme change request
    Core->>TM: Apply theme
    
    TM->>TM: Load theme definition
    TM->>TM: Process theme variables
    TM-->>Core: Theme processed
    
    Core->>RE: Update rendering
    RE->>RE: Apply theme styles
    RE-->>Core: Visual update complete
    
    Core->>Store: Save theme preference
    Store-->>Core: Save confirmation
    
    Core->>UI: Update interface colors
    UI-->>User: Display new theme
```

## Offline Sync Flow

```mermaid
sequenceDiagram
    actor User
    participant App as Application
    participant Core as Core Engine
    participant Sync as Sync Manager
    participant Cache as Cache Manager
    participant Cloud as Cloud Storage
    
    Note over User, Cloud: Going Offline
    
    App->>Core: Connection lost event
    Core->>Sync: Enter offline mode
    Sync->>Sync: Mark pending changes
    Sync-->>Core: Offline mode active
    Core->>UI: Update connection status
    UI-->>User: Show offline indicator
    
    Note over User, Cloud: Working Offline
    
    User->>UI: Continue working
    UI->>Core: User actions
    Core->>Cache: Store changes locally
    Cache-->>Core: Changes cached
    
    Note over User, Cloud: Coming Back Online
    
    App->>Core: Connection restored event
    Core->>Sync: Resume online mode
    Sync->>Sync: Check for pending changes
    
    alt Pending Changes Exist
        Sync->>Cloud: Upload changes
        Cloud-->>Sync: Upload confirmation
        
        alt Conflicts Detected
            Cloud->>Sync: Conflict notification
            Sync->>UI: Show conflict resolution
            UI-->>User: Display conflict options
            User->>UI: Resolve conflicts
            UI->>Sync: Resolution decisions
            Sync->>Cloud: Apply resolutions
            Cloud-->>Sync: Resolution confirmation
        end
        
        Sync-->>Core: Sync complete
    end
    
    Core->>UI: Update connection status
    UI-->>User: Show online indicator
```

## Print/Export Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as User Interface
    participant Core as Core Engine
    participant Exp as Export Manager
    participant RE as Render Engine
    participant FS as File System
    
    User->>UI: Request print/export
    UI->>Core: Print/export request
    Core->>Exp: Initialize export
    
    alt Print Document
        Exp->>RE: Generate print version
        RE->>RE: Apply print styles
        RE->>RE: Format for printing
        RE-->>Exp: Print-ready content
        Exp->>Exp: Send to printer dialog
        Exp-->>Core: Print initiated
        Core->>UI: Show print dialog
        UI-->>User: Print options
        
    else Export as PDF
        Exp->>RE: Generate PDF version
        RE->>RE: Format for PDF
        RE-->>Exp: PDF-ready content
        Exp->>Exp: Generate PDF file
        Exp->>FS: Save PDF
        FS-->>Exp: Save confirmation
        Exp-->>Core: Export complete
        Core->>UI: Show completion
        UI-->>User: PDF saved notification
        
    else Export as Other Format
        Exp->>Exp: Convert to target format
        Exp->>FS: Save file
        FS-->>Exp: Save confirmation
        Exp-->>Core: Export complete
        Core->>UI: Show completion
        UI-->>User: File saved notification
    end
```

## Plugin Loading Flow

```mermaid
sequenceDiagram
    participant App as Application Startup
    participant Core as Core Engine
    participant PS as Plugin System
    participant PM as Plugin Manager
    participant Storage as Plugin Storage
    participant EP as External Plugin
    
    App->>Core: Initialize
    Core->>PS: Load plugins
    
    PS->>Storage: Get enabled plugins
    Storage-->>PS: Enabled plugin list
    
    PS->>PM: Discover plugins
    PM->>PM: Scan plugin directories
    
    loop For each plugin
        PM->>PM: Validate plugin
        PM->>PM: Check compatibility
        
        alt Plugin Valid
            PM->>EP: Load plugin
            EP-->>PM: Register capabilities
            PM->>PM: Register extension points
            PM-->>PS: Plugin loaded
        else Plugin Invalid
            PM->>PM: Log error
            PM->>Storage: Mark as disabled
            PM-->>PS: Plugin skipped
        end
    end
    
    PS-->>Core: Plugin loading complete
    Core->>App: Initialization complete
    
    Note over App, EP: Later, during operation
    
    Core->>PS: Use plugin functionality
    PS->>EP: Execute plugin method
    EP-->>PS: Return result
    PS-->>Core: Plugin result
```

## Tab Group Management Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as User Interface
    participant Core as Core Engine
    participant TE as Tab Engine
    participant TG as Tab Group Manager
    participant PM as Project Manager
    
    User->>UI: Select multiple tabs
    UI->>Core: Tab selection
    Core->>TE: Get selected tabs
    TE-->>Core: Selected tab list
    
    User->>UI: Create tab group
    UI->>Core: Create group request
    Core->>TG: Create new group
    TG->>TG: Generate group ID
    TG->>TG: Assign tabs to group
    TG-->>Core: Group created
    
    Core->>TE: Update tab display
    TE-->>Core: Display updated
    Core->>UI: Show grouped tabs
    UI-->>User: Display tab group
    
    User->>UI: Save as project
    UI->>Core: Save as project
    Core->>PM: Create project from group
    PM->>PM: Generate project structure
    PM->>PM: Include tab references
    PM->>PM: Add metadata
    PM-->>Core: Project created
    
    Core->>UI: Show save dialog
    UI-->>User: File save options
    User->>UI: Confirm save
    UI->>Core: Save confirmation
    Core->>PM: Save project file
    PM-->>Core: Project saved
    Core->>UI: Show confirmation
    UI-->>User: Project saved notification
```

## Settings Management Flow

```mermaid
sequenceDiagram
    actor User
    participant UI as User Interface
    participant Core as Core Engine
    participant SM as Settings Manager
    participant Storage as Settings Storage
    participant App as Application Components
    
    User->>UI: Open settings
    UI->>Core: Settings request
    Core->>SM: Get current settings
    SM->>Storage: Load settings
    Storage-->>SM: Settings data
    SM-->>Core: Settings structure
    Core->>UI: Display settings
    UI-->>User: Show settings UI
    
    User->>UI: Modify settings
    UI->>Core: Update settings
    Core->>SM: Apply changes
    SM->>SM: Validate settings
    SM->>Storage: Save settings
    Storage-->>SM: Save confirmation
    
    SM->>SM: Identify affected components
    
    loop For each affected component
        SM->>App: Notify setting change
        App->>App: Apply new setting
        App-->>SM: Setting applied
    end
    
    SM-->>Core: Settings updated
    Core->>UI: Refresh interface
    UI-->>User: Show updated UI
```

These sequence diagrams illustrate the primary workflows within the MarkDocViewer application, showing how different components interact to accomplish various tasks. The flows are designed to be modular, maintainable, and extensible, allowing for future enhancements while maintaining a consistent user experience across all platforms.
