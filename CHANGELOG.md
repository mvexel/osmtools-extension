# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2024-12-28

### Added
- **Link Opening Behavior Setting**: Users can now choose how tool links open:
  - **Open in new tab** (default) - Better for tiling window managers
  - **Open in same tab** - Minimal screen space usage
  - **Open in new window** - Original behavior
- Global settings section in the settings page
- Auto-save functionality for global settings changes

### Changed
- **Default behavior**: Links now open in new tabs instead of new windows by default
- Reorganized settings page with separate sections for general settings and tool configuration
- Improved popup closing behavior based on selected link opening method

### Fixed
- Enhanced navigation handling for same-tab link opening
- Proper initialization of global settings for new and existing users

### Technical
- Added `defaultGlobalSettings` object in defaults.js
- Updated storage initialization to handle global settings
- Enhanced settings UI with dropdown for link behavior selection
- Modified reset functionality to include global settings

## [1.0.1] - Previous Release

### Initial Features
- Quick access popup for OSM tools
- Support for coordinate-based tools (map links)
- Support for changeset inspection tools
- Drag-and-drop tool reordering
- Enable/disable individual tools
- Add custom tools functionality
- Settings page for tool management
- Storage sync across browser instances