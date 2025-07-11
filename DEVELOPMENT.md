# Development Guide

This guide will help you set up the OSM Tools Extension for local development and testing in both Firefox and Chrome.

## Prerequisites

- Firefox Developer Edition (recommended) or Firefox 109+
- Chrome/Chromium browser
- Basic knowledge of web extensions

## Project Structure

```
osmtools-extension/
├── chrome/                 # Extension source code
│   ├── manifest.json      # Extension manifest
│   ├── popup.html         # Main popup interface
│   ├── popup.js           # Popup logic
│   ├── settings.html      # Settings page
│   ├── settings.js        # Settings logic
│   ├── defaults.js        # Default tools configuration
│   ├── reset-storage.js   # Storage reset functionality
│   └── icons/             # Extension icons
├── CHANGELOG.md           # Version history
├── DEVELOPMENT.md         # This file
└── README.md              # Project documentation
```

## Local Development Setup

### For Chrome/Chromium

1. **Open Chrome Extensions Page**
   - Navigate to `chrome://extensions/`
   - Enable "Developer mode" (toggle in top right)

2. **Load the Extension**
   - Click "Load unpacked"
   - Select the `osmtools-extension/chrome` directory
   - The extension should appear in your extensions list

3. **Testing**
   - Navigate to an OpenStreetMap page with coordinates (e.g., `https://www.openstreetmap.org/#map=15/52.5200/13.4050`)
   - Click the extension icon in the toolbar
   - Test different link opening behaviors in settings

4. **Debugging**
   - Right-click the extension icon → "Inspect popup" to debug popup.js
   - Use Chrome DevTools for the settings page
   - Check `chrome://extensions/` for error messages

### For Firefox

1. **Open Firefox Add-ons Debug Page**
   - Navigate to `about:debugging`
   - Click "This Firefox" in the sidebar

2. **Load the Extension**
   - Click "Load Temporary Add-on"
   - Select the `manifest.json` file from `osmtools-extension/chrome/`
   - The extension should appear in your temporary extensions

3. **Testing**
   - Navigate to an OpenStreetMap page with coordinates
   - Click the extension icon in the toolbar
   - Test functionality and settings

4. **Debugging**
   - Use the "Inspect" button next to the extension in about:debugging
   - Check the Browser Console for errors (`Ctrl+Shift+J`)

## Making Changes

### Adding New Tools

1. **Edit `defaults.js`**
   ```javascript
   'New Tool Name': {
       url: 'https://example.com/tool?lat={lat}&lon={lon}&zoom={zoom}',
       enabled: true,
       type: 'coordinate' // or 'changeset'
   }
   ```

2. **Test the Changes**
   - Reload the extension in your browser
   - Clear extension storage (use Reset button) to see new defaults
   - Verify the new tool appears in settings and popup

### Modifying UI/Behavior

1. **HTML Changes**: Edit `popup.html` or `settings.html`
2. **JavaScript Changes**: Edit `popup.js` or `settings.js`
3. **Styling**: Modify the `<style>` sections in HTML files

### Testing Link Opening Behavior

1. **Configure Test Environment**
   - Set up a tiling window manager (if testing the original issue)
   - Or use browser developer tools to simulate different environments

2. **Test All Three Modes**
   - New tab (default)
   - Same tab
   - New window

3. **Verify Expected Behavior**
   - New tab: Opens in new tab, popup closes
   - Same tab: Opens in current tab, popup closes
   - New window: Opens in new window/tab (browser dependent), popup closes

## Reloading Changes

### Chrome
- Go to `chrome://extensions/`
- Click the reload button (↻) for the extension
- Or use `Ctrl+R` while focused on the extensions page

### Firefox
- Go to `about:debugging`
- Click "Reload" next to the extension
- Or remove and re-add the extension

## Common Issues and Solutions

### Extension Not Loading
- **Check manifest.json syntax**: Use a JSON validator
- **Verify file paths**: Ensure all referenced files exist
- **Check permissions**: Make sure manifest has required permissions

### Popup Not Showing Tools
- **Check browser console**: Look for JavaScript errors
- **Verify URL matching**: Test with known working OSM URLs
- **Check storage**: Use browser dev tools to inspect `chrome.storage.sync`

### Settings Not Saving
- **Check storage permissions**: Ensure "storage" permission in manifest
- **Verify Chrome sync**: Settings use `chrome.storage.sync`
- **Test storage operations**: Use browser dev tools console

### Reset Storage (for testing)
- Use the "Reset to Defaults" button in the popup
- Or manually clear storage via browser dev tools:
  ```javascript
  chrome.storage.sync.clear()
  ```

## Testing Checklist

Before submitting changes:

- [ ] Extension loads without errors in Chrome
- [ ] Extension loads without errors in Firefox
- [ ] Popup displays correctly on OSM coordinate URLs
- [ ] Popup displays correctly on changeset URLs
- [ ] Settings page loads and saves correctly
- [ ] All three link opening behaviors work as expected
- [ ] Drag-and-drop reordering works in settings
- [ ] Enable/disable toggles work for individual tools
- [ ] Custom tool addition works
- [ ] Reset to defaults works
- [ ] No console errors in normal usage

## Browser Compatibility

- **Chrome**: 88+ (Manifest V3 requirement)
- **Firefox**: 109+ (specified in manifest)
- **Edge**: Should work with Chrome instructions
- **Safari**: Not currently supported (different extension format)

## Debugging Tips

1. **Enable verbose logging**
   ```javascript
   console.log('Debug info:', variable);
   ```

2. **Inspect storage**
   ```javascript
   chrome.storage.sync.get(null, (data) => console.log(data));
   ```

3. **Test URL patterns**
   - Use regex testers for URL matching patterns
   - Test with various OSM URL formats

4. **Simulate different scenarios**
   - Test with no coordinates in URL
   - Test with malformed URLs
   - Test with different zoom levels

## Contributing

1. Make your changes following the patterns in existing code
2. Test in both Chrome and Firefox
3. Update this guide if you add new features
4. Update CHANGELOG.md with your changes
5. Submit a pull request with a clear description

## Resources

- [Chrome Extension Documentation](https://developer.chrome.com/docs/extensions/)
- [Firefox Extension Documentation](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions)
- [Manifest V3 Migration Guide](https://developer.chrome.com/docs/extensions/migrating/)