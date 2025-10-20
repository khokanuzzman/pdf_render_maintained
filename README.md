# pdf_render_maintained

[![pub package](https://img.shields.io/pub/v/pdf_render_maintained.svg)](https://pub.dev/packages/pdf_render_maintained)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A maintained fork of the original `pdf_render` plugin that provides intermediate PDF rendering APIs and easy-to-use Flutter Widgets. This package is inspired by and based on the excellent work by [espresso3389](https://github.com/espresso3389).

## ⚠️ Important Notice

This package is a **maintained fork** of the original [pdf_render](https://pub.dev/packages/pdf_render) package by [espresso3389](https://github.com/espresso3389). The original package is no longer actively maintained, so this fork provides:

- ✅ **Active maintenance** and bug fixes
- ✅ **Updated dependencies** for modern Flutter versions
- ✅ **Compatibility** with latest Flutter SDK (3.0+)
- ✅ **Same API** - drop-in replacement for the original package
- ✅ **All platforms** supported (iOS, Android, macOS, Web)

### Original Package Attribution

This package is based on the original work by [espresso3389](https://github.com/espresso3389) and the [pdf_render](https://pub.dev/packages/pdf_render) package. We are grateful for their excellent work and maintain this fork to keep the package alive for the Flutter community.

**Original Repository**: https://github.com/espresso3389/flutter_pdf_render  
**Original Package**: https://pub.dev/packages/pdf_render  
**Original Author**: [espresso3389](https://github.com/espresso3389)

## Features

- 📱 **Multi-platform support**: iOS, Android, macOS, and Web
- 🎨 **Easy-to-use widgets**: `PdfViewer`, `PdfDocumentLoader`, `PdfPageView`
- ⚡ **High-performance rendering**: Direct texture rendering for smooth performance
- 🔧 **Flexible APIs**: Both widget-based and low-level rendering APIs
- 📄 **Multiple sources**: Load from assets, files, or memory data
- 🎯 **Interactive viewing**: Pinch-zoom, pan, and navigation controls

## Installation

Add this to your package's `pubspec.yaml` file:

```yaml
dependencies:
  pdf_render_maintained: ^1.5.0
```

Then run `flutter pub get`.

### Web Setup

For Web support, add the following script tags to your `index.html` before the main.dart.js script:

```html
<!-- IMPORTANT: load pdfjs files -->
<script
  src="https://cdn.jsdelivr.net/npm/pdfjs-dist@3.4.120/build/pdf.min.js"
  type="text/javascript"
></script>
<script type="text/javascript">
  pdfjsLib.GlobalWorkerOptions.workerSrc =
    "https://cdn.jsdelivr.net/npm/pdfjs-dist@3.4.120/build/pdf.worker.min.js";
  pdfRenderOptions = {
    cMapUrl: "https://cdn.jsdelivr.net/npm/pdfjs-dist@3.4.120/cmaps/",
    cMapPacked: true,
  };
</script>
```

## Quick Start

### Simple PDF Viewer

```dart
import 'package:pdf_render_maintained/pdf_render_widgets.dart';

@override
Widget build(BuildContext context) {
  return MaterialApp(
    home: Scaffold(
      appBar: AppBar(title: const Text('PDF Viewer')),
      body: PdfViewer.openAsset('assets/hello.pdf'),
    ),
  );
}
```

### Advanced Usage with Controller

```dart
import 'package:pdf_render_maintained/pdf_render_widgets.dart';

class MyPdfViewer extends StatefulWidget {
  @override
  _MyPdfViewerState createState() => _MyPdfViewerState();
}

class _MyPdfViewerState extends State<MyPdfViewer> {
  PdfViewerController? controller;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('PDF Viewer')),
      body: PdfViewer.openAsset(
        'assets/hello.pdf',
        params: PdfViewerParams(
          onViewerControllerInitialized: (PdfViewerController c) {
            controller = c;
          },
        ),
      ),
      floatingActionButton: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          FloatingActionButton(
            child: Icon(Icons.first_page),
            onPressed: () => controller?.ready?.goToPage(pageNumber: 1),
          ),
          FloatingActionButton(
            child: Icon(Icons.last_page),
            onPressed: () => controller?.ready?.goToPage(pageNumber: controller?.pageCount ?? 1),
          ),
        ],
      ),
    );
  }
}
```

## API Overview

### Widgets

- **`PdfViewer`**: Full-featured PDF viewer with zoom, pan, and navigation
- **`PdfDocumentLoader`**: Loads and manages PDF documents
- **`PdfPageView`**: Renders individual PDF pages

### Core APIs

- **`PdfDocument`**: Main document class for PDF operations
- **`PdfPage`**: Individual page representation
- **`PdfPageImage`**: Rendered page image data
- **`PdfPageImageTexture`**: High-performance texture rendering

## Migration from Original Package

If you're migrating from the original `pdf_render` package, simply change your import:

```dart
// Old import
import 'package:pdf_render/pdf_render.dart';
import 'package:pdf_render/pdf_render_widgets.dart';

// New import
import 'package:pdf_render_maintained/pdf_render.dart';
import 'package:pdf_render_maintained/pdf_render_widgets.dart';
```

And update your `pubspec.yaml`:

```yaml
dependencies:
  pdf_render_maintained: ^1.5.0  # Instead of pdf_render: ^1.4.12
```

## Contributing

We welcome contributions! Please feel free to submit issues and pull requests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Original package by [espresso3389](https://github.com/espresso3389)
- PDF.js by Mozilla for Web support
- The Flutter community for their continued support

---

**Note**: This package maintains compatibility with the original `pdf_render` API while providing active maintenance and updates for modern Flutter versions.