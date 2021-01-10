# Unity-CI image of the Unity Editor (cleaned)

#### `unity-ci/editor-lite`

Dockerised Unity Editor made for continuous integration.
Additionally from the Editor removed a lot of content to reduce image size.

## Know Limitations

This image doesn't contain the full version of Unity Editor, so it's not possible
to do some operations on it. There is a list of known limitations:

- ...

## Usage

Run the editor image using an interactive shell

```bash
docker run -it --rm unityci/editor-lite:[tag] bash
```
example

```bash
docker run -it --rm unityci/editor-lite:ubuntu-2020.1.1f1-android-0.3.0 bash
```

Run the editor 

```bash
unity-editor help
```

## License

[MIT license](https://github.com/game-ci/docker/blob/main/LICENSE)

