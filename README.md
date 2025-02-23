# MrSolimanKing/react-native-draw

[![NPM badge](https://img.shields.io/npm/v/@benjeau/react-native-draw)](https://www.npmjs.com/package/@benjeau/react-native-draw) [![CircleCI Status](https://img.shields.io/circleci/build/gh/BenJeau/react-native-draw)](https://app.circleci.com/pipelines/github/BenJeau/react-native-draw) ![Platform badge](https://img.shields.io/badge/platform-android%20%7C%20ios%20%7C%20web-blue)

Cross-platform React Native drawing component based on SVG

> Note: Performance may not be great, this is not my main focus right now, but will be tackled via resolving this [issue](https://github.com/BenJeau/react-native-draw/issues/4)

![Drawing Example](assets/drawingExample.gif)

Example application with React Native performance overlay

## Installation

```sh
npm install MrSolimanKing/react-native-draw
# or
yarn add MrSolimanKing/react-native-draw
```

> Also, you need to install [react-native-gesture-handler](https://github.com/software-mansion/react-native-gesture-handler), [@react-native-community/slider](https://github.com/callstack/react-native-slider) and [react-native-svg](https://github.com/react-native-svg/react-native-svg), and follow their installation instructions.

## Usage

```tsx
import React from 'react';
import { Draw, DrawRef } from "@benjeau/react-native-draw";

export default function App() {
  const drawRef = useRef<DrawRef>(null);

  const removeLastPath = () {
    drawRef.current.?undo();
  }

  const clearDrawing = () {
    drawRef.current.?clear();
  }

  // ... for more ref functions, look below

  return (
    <Draw
      ref={drawRef}
      height={400}
      width={300}
      initialValues={{
        color: "#B644D0",
        thickness: 10,
        opacity: 0.5,
        paths: []
      }}
      brushPreview="none"
      canvasStyle={{ elevation: 0, backgroundColor: "red" }}
    />
  )
}
```

## Props

All of the props are optional

| name                     | description                                                                                | type                                           | default                                |
| ------------------------ | ------------------------------------------------------------------------------------------ | ---------------------------------------------- | -------------------------------------- |
| `colors`                 | Color palette colors, specifying the color palette sections each containing rows of colors | `string[][][]`                                 | [`DEFAULT_COLORS`](./src/constants.ts) |
| `height`                 | Height of the canvas                                                                       | `number`                                       | height of the window - 80              |
| `width`                  | Width of the canvas                                                                        | `number`                                       | width of the window                    |
| `autoDismissColorPicker` | Automatically close the color picker after selecting a color                               | `boolean`                                      | `false`                                |
| `initialValues`          | Initial values for color the brush and paths                                               | [`DrawInitialValues`](./src/Draw.tsx)          | see [below](#DrawInitialValues)        |
| `hideBottom`             | Hide all of the bottom section, below the canvas, or only certain functionalities          | `boolean` or `HideBottom`                      | false                                  |
| `brushPreview`           | Change brush preview preset or remove it                                                   | `stroke` or `dot` or `none`                    | `stroke`                               |
| `simplifyOptions`        | SVG simplification options                                                                 | [`SimplifyOptions`](./src/Draw.tsx)            | see [below](#SimplifyOptions)          |
| `canvasStyle`            | Override the style of the container of the canvas                                          | `StyleProp`                                    | -                                      |
| `buttonStyle`            | Override the style of the buttons                                                          | `StyleProp`                                    | -                                      |
| `onPathsChange`          | Callback function when paths change                                                        | (paths: [`PathType`](./src/types.ts)[]) => any | -                                      |
| `eraserSize`             | Width of eraser (to compensate for path simplification)                                    | `number`                                       | `5`                                    |
| `isBrushActive`          | activate or deactivate the brush                                                           | `boolean`                                      | `false`                                |
### DrawInitialValues

| name        | description                                   | type          | default                                                             |
| ----------- | --------------------------------------------- | ------------- | ------------------------------------------------------------------- |
| `color`     | Initial brush color, from the colors provided | `string`      | the first color of the first row in the first section from `colors` |
| `thickness` | Initial thickness of the brush strokes        | `number`      | `3`                                                                 |
| `opacity`   | Initial opacity of the brush strokes          | `number`      | `1`                                                                 |
| `paths`     | Paths to be already drawn                     | `PathType[]`  | `[]`                                                                |
| `tool`      | Initial tool of the canvas                    | `DrawingTool` | `brush`                                                             |

### SimplifyOptions

| name                  | description                                                                   | type      | default |
| --------------------- | ----------------------------------------------------------------------------- | --------- | ------- |
| `simplifyPaths`       | Enable SVG path simplification on paths, except the one currently being drawn | `boolean` | `true`  |
| `simplifyCurrentPath` | Enable SVG path simplification on the stroke being drawn                      | `boolean` | `false` |
| `amount`              | Amount of simplification to apply                                             | `number`  | `10`    |
| `roundPoints`         | Ignore fractional part in the points. Improves performance                    | `boolean` | `true`  |

## Ref functions

| name       | description                                | type                               |
| ---------- | ------------------------------------------ | ---------------------------------- |
| `setColor` | Set the brush color                        | `Dispatch<SetStateAction<string>>` |
| `undo`     | Undo last brush stroke                     | `() => void`                       |
| `clear`    | Removes all brush strokes                  | `() => void`                       |
| `getPaths` | Get brush strokes data                     | `() => PathType[]`                 |
| `addPath`  | Append a path to the current drawing paths | `(path: PathType) => void`         |
| `getSvg`   | Get SVG path string of the drawing         | `() => string`                     |

## Helper functions

* If you need to create an SVG path, `createSVGPath()` is available to create the string representation of an SVG path.

## Contributing

See the [contributing guide](CONTRIBUTING.md) to learn how to contribute to the repository and the development workflow.

## License

MIT
