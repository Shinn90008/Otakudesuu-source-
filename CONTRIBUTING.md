# Contributing to Otakudesu Extension

This guide explains how to contribute to the **Otakudesu Mangayomi Extension** project.

## About This Extension

This is a **Dart extension** for the **Mangayomi** application that provides access to anime content from **Otakudesu.blog**.

- **Base URL**: https://otakudesu.blog
- **Type**: Anime Source
- **Language**: Indonesian (id)

## Prerequisites

Before contributing, ensure you have:

1. The latest **Mangayomi** application installed (desktop version recommended)
2. Basic understanding of **Dart** programming language
3. Git and GitHub account

## Extension Methods

This extension implements the following core methods:

### 1. **getPopular(int page)**
- Returns popular anime from the ongoing anime section
- Supports pagination
- Returns: `MPages` with list of `MManga` entries

### 2. **getLatest(int page)**
- Returns the latest episodes
- Supports pagination
- Returns: `MPages` with list of `MManga` entries

### 3. **search(String query, int page, List<dynamic> filters)**
- Searches for anime by title
- Supports pagination and filters
- Returns: `MPages` with search results

### 4. **getDetail(MManga manga)**
- Retrieves detailed information about an anime
- Fetches all episodes/chapters
- Returns: Complete `MManga` object with chapters

### 5. **getVideoList(MChapter chapter)**
- Retrieves video links for an episode
- Returns: List of `MVideo` objects with streaming URLs

### 6. **getFilterList()**
- Returns available search filters
- Currently returns empty list (can be extended)

## Data Models

### MManga
```dart
class MManga {
  final String title;           // Anime title
  final String url;             // Anime URL
  final String imageUrl;        // Poster image URL
  final String? description;    // Anime description
  final String? author;         // Studio/Producer
  final List<String>? genre;    // List of genres
  final Status? status;         // Ongoing, Completed, etc.
  final List<MChapter>? chapters; // Episodes list
}
```

### MChapter
```dart
class MChapter {
  final String name;            // Episode name/number
  final String url;             // Episode URL
  final int? dateUpload;        // Timestamp in milliseconds
  final String? scanlator;      // Uploader info
}
```

### MVideo
```dart
class MVideo {
  final String url;             // Streaming URL
  final String quality;         // Quality/Source label
  final Map<String, String>? headers; // HTTP headers
}
```

### MPages
```dart
class MPages {
  final List<MManga> manga;     // List of anime
  final bool hasNextPage;       // Pagination indicator
}
```

## Status Enum

Supported anime statuses:
- `Status.ongoing` - Currently airing
- `Status.completed` - Finished
- `Status.hiatus` - On break
- `Status.canceled` - Cancelled
- `Status.publishingFinished` - Finished airing
- `Status.unknown` - Unknown status

## Available Helper Functions

The Mangayomi framework provides these utilities:

### HTTP Client
```dart
final Client client = Client();
final res = await client.get(
  Uri.parse('https://example.com'),
  headers: {'Referer': 'https://otakudesu.blog'}
);
```

### HTML Parsing
```dart
// Using parseHtml to get MDocument
final MDocument document = parseHtml(res.body);

// Select first element
final MElement? element = document.selectFirst('.anime-title');

// Select multiple elements
final List<MElement> elements = document.select('.anime-item');

// Get attributes
final String? href = element?.attr('href');
final String? title = element?.attr('title');

// Get text content
final String text = element?.text ?? '';
```

### String Utilities
- `substringAfter(String text, String pattern)`
- `substringAfterLast(String text, String pattern)`
- `substringBefore(String text, String pattern)`
- `substringBeforeLast(String text, String pattern)`
- `getUrlWithoutDomain(String url)`

## Getting Started with Development

### Step 1: Test in Mangayomi App
1. Open Mangayomi application
2. Go to **Extensions** tab
3. Click **+** to create new extension
4. Fill in:
   - **Name**: Otakudesu
   - **Base URL**: https://otakudesu.blog
   - **Language**: id (Indonesian)
5. Click **Save**

### Step 2: Edit in Browser
1. Click the extension to open settings
2. Click **Edit Code**
3. You'll see three panels:
   - **Code Editor**: Write your Dart code
   - **Fetch Result**: Test your methods
   - **Console**: View logs and errors

### Step 3: Test Methods
Use the "Fetch result" panel to test:
- `getPopular(1)` - Test popular anime
- `getLatest(1)` - Test latest episodes
- `search('naruto', 1, [])` - Test search
- `getDetail(manga)` - Test details
- `getVideoList(chapter)` - Test video links

## Common Issues & Solutions

### Issue: Cannot find elements
**Solution**: Check CSS selectors are correct using browser DevTools

### Issue: Videos not loading
**Solution**: Verify iframe sources and streaming URLs

### Issue: Date parsing fails
**Solution**: Use `parseDates()` helper with correct format string

### Issue: Pagination not working
**Solution**: Verify URL pattern changes with page number

## How to Submit Changes

1. **Fork** this repository
2. **Create** a feature branch: `git checkout -b improve/feature-name`
3. **Test** thoroughly in Mangayomi
4. **Commit** with clear messages: `git commit -m "Add feature description"`
5. **Push** to your fork: `git push origin improve/feature-name`
6. **Create a Pull Request** with description of changes

## Pull Request Guidelines

When submitting a PR, include:

- [ ] Clear description of changes
- [ ] Testing performed in Mangayomi
- [ ] No breaking changes
- [ ] Code follows Dart style guide
- [ ] Updated documentation if needed

## Testing Checklist

Before submitting:

- [ ] `getPopular()` returns anime list
- [ ] `getLatest()` returns recent episodes
- [ ] `search()` works with queries
- [ ] `getDetail()` loads all info correctly
- [ ] `getVideoList()` returns valid video links
- [ ] No console errors
- [ ] Images load properly

## Documentation

The extension code includes detailed comments explaining:
- What each method does
- Parameter descriptions
- Return value formats
- Error handling

## Need Help?

- Join the **Mangayomi Discord**: https://discord.com/invite/EjfBuYahsP
- Check **Mangayomi Documentation**: https://docs.mangayomi.com
- Review **existing extensions** for examples

## License

This project is licensed under the **MIT License** - see LICENSE file for details.

---

**Happy coding! 🚀**
