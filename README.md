# Robot AR Visualisation

A browser-based image-tracking AR page. It uses MindAR to show a live camera
view, scan the Approach, Line, and Square target images, and display an animated
GIF on the detected image.

## Run locally

Camera access requires a secure browser context: use `localhost` for local
testing or serve the page over HTTPS when accessing it from another device.
Opening `index.html` directly as a `file://` URL may prevent camera access.

For example, with Python installed, run this from the project directory:

```powershell
py -m http.server 8000
```

Then open <http://localhost:8000> in a supported browser, allow camera access,
and point the camera at one of the target images. On a phone, deploy the files
to an HTTPS web host and open the hosted page on the phone.

## Targets and assets

The page uses `targets.mind` as its MindAR image-target database. The target
indexes in `index.html` are:

| Target index | Image | Animation |
| --- | --- | --- |
| 0 | `Approach.png` | `Approach.gif` |
| 1 | `Line.png` | `Line.gif` |
| 2 | `Square.png` | `Square.gif` |

Keep the target order in `targets.mind` consistent with these indexes. The
individual `approach.mind`, `Line.mind`, and `Square.mind` files are also
included, but the page currently loads the combined `targets.mind` file.

The page's image and animation files are present beside `index.html`.

## Implementation

- `index.html` contains the scene, camera startup, target tracking, and GIF
  texture component.
- A-Frame 1.5.0, MindAR 1.2.5, and gifler 0.1.0 are loaded from CDNs, so the
  page needs an internet connection.
- The status message reports camera startup and target detection. If the camera
  does not start, check browser camera permissions and serve the page from a
  secure context.
