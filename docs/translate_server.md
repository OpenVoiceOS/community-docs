# OpenVoiceOS Translate Server

Turn any OVOS Language plugin into a microservice!

Use with OpenVoiceOS [companion plugin](https://github.com/OpenVoiceOS/ovos-translate-server-plugin)

## Install

`pip install ovos-translate-server`

## Usage

```bash
ovos-translate-server --help
usage: ovos-translate-server [-h] [--tx-engine TX_ENGINE]
                   [--detect-engine DETECT_ENGINE] [--port PORT] [--host HOST]

optional arguments:
  -h, --help            show this help message and exit
  --tx-engine TX_ENGINE
                        translate plugin to be used
  --detect-engine DETECT_ENGINE
                        lang detection plugin to be used
  --port PORT           port number
  --host HOST           host

```

eg, to use the [Google Translate plugin](https://github.com/NeonGeckoCom/neon-lang-plugin-google_translate) `ovos-translate-server --tx-engine googletranslate_plug --detect-engine googletranslate_detection_plug`

then you can do get requests

- `http://0.0.0.0:9686/translate/en/o meu nome é Casimiro` (auto detect source lang)
- `http://0.0.0.0:9686/translate/pt/en/o meu nome é Casimiro`  (specify source lang)
- `http://0.0.0.0:9686/detect/o meu nome é Casimiro`

## Docker Template

you can create easily crete a docker file to serve any plugin

```dockerfile
FROM python:3.7

RUN pip3 install ovos-utils==0.0.15
RUN pip3 install ovos-plugin-manager==0.0.4
RUN pip3 install ovos-translate-server==0.0.1

RUN pip3 install {PLUGIN_HERE}

ENTRYPOINT ovos-translate-server --tx-engine {PLUGIN_HERE} --detect-engine {PLUGIN_HERE}
```

build it
```bash
docker build . -t my_ovos_translate_plugin
```

run it
```bash
docker run -p 8080:9686 my_ovos_translate_plugin
```

Each plugin can provide its own Dockerfile in its repository using ovos-translate-server