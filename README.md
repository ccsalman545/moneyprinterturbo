# Run MoneyPrinterTurbo on Google Colab

This notebook installs [MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) in an isolated Python 3.11 environment and launches its WebUI. Colab runtimes are temporary, so generated files are removed when the runtime is reset.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ccsalman545/moneyprinterturbo/blob/main/docs/MoneyPrinterTurbo.ipynb)

MoneyPrinterTurbo turns a topic or keyword into an HD short video: it writes a script, matches stock footage, synthesizes a voiceover, burns in subtitles, and mixes background music.

## Open the notebook

1. Click **Open in Colab** above, or open [`docs/MoneyPrinterTurbo.ipynb`](docs/MoneyPrinterTurbo.ipynb) from this repository.
2. In Colab: **Runtime → Run all**.
3. When prompted, paste your [ngrok authtoken](https://dashboard.ngrok.com/get-started/your-authtoken). The token is read with `getpass` and is not written into the notebook.
4. Open the printed public URL. If ngrok shows an interstitial page, click **Visit Site**.
5. In the WebUI **Settings** panel, add an LLM API key and a footage-source key, then generate a video.

## What the notebook does

| Step | Cell | Purpose |
| --- | --- | --- |
| 1 | Install | Clones or updates `harry0703/MoneyPrinterTurbo`, installs `uv` + `pyngrok`, then runs `uv sync --frozen --python 3.11` in a project virtualenv |
| 2 | Tunnel | Authenticates ngrok so the remote Streamlit server can be opened from your browser |
| 3 | Launch | Starts `uv run streamlit run webui/Main.py` on port `8501`, waits for `/_stcore/health`, then prints the public HTTPS URL |
| Optional | Drive | Copies `/content/MoneyPrinterTurbo/storage/` to Google Drive before the runtime is wiped |
| Optional | Stop | Terminates Streamlit and closes ngrok tunnels |

The install uses MoneyPrinterTurbo's lockfile and does not replace Colab's preinstalled packages. System tools (`ffmpeg`, ImageMagick) are installed only when they are missing.

## What you need

- A Google account (free Colab is enough; a GPU is optional)
- A free [ngrok](https://dashboard.ngrok.com/signup) account
- An LLM provider key (OpenAI, Gemini, DeepSeek, Moonshot, Groq, and others are supported in the WebUI)
- A [Pexels](https://www.pexels.com/api/), [Pixabay](https://pixabay.com/api/docs/), or [Coverr](https://coverr.co/developers) API key unless you upload local footage

Edge TTS can narrate without a paid speech key.

## Persistence

Colab disks are deleted when the runtime resets, disconnects, or idle-timeouts. Download finished videos from the WebUI, or run the optional Drive cell to copy `storage/` to `MyDrive/MoneyPrinterTurbo/storage`.

## Upstream project

This repository hosts the Colab runner. The application itself lives at [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo).
