# IRIS | Assistive Vision Prototype

IRIS is a local scene-description prototype developed by a fourth-year INSA Lyon SMART team. It collects webcam frames, uses scene changes to schedule inference, combines observations from different model adapters, and presents descriptions through speech and a browser interface. Rime Chihab-Eddine contributed the initial architecture in revision `cdcea6f`.

## Start the local web app

Use Python 3.11 or 3.12. From the repository root:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m uvicorn Moteur.api_server:app --host 127.0.0.1 --port 8000
```

On Windows, activate with `.venv\Scripts\Activate.ps1`. Open `http://127.0.0.1:8000`. The homepage and `/api/status` can be checked before connecting a camera or loading any models.

## Run live inference

Start Ollama locally and pull the configured models:

```bash
ollama pull llava-phi3
ollama pull llama3.2
```

Place compatible YOLO, YuNet and SFace weights under `models/` using the filenames in `Moteur/config/iris.yaml`, or change the configured paths. The scene gate can download its optional MobileNet model. Select a webcam and start the pipeline from the web app. On Linux, speech output requires a system speech engine such as eSpeak.

The web service is intended for local demonstrations. Camera enrollment and face data are stored under `data/`. Use only consenting participants.

## Source and credits

`Moteur/core/` holds the orchestrator, data pool and scene gate. `Moteur/adapters/` integrates model-specific inference. `Moteur/api_server.py` connects the local pipeline to `interface/`.

This source snapshot is based on [the team's IRIS repository](https://github.com/hdnys/IRIS) at revision `b5c4461` and retains the original [CC0 license](LICENSE). Team contributors include Nour205, Elie-Hasbani, Liam Le Touzé, Mohamad2305, Ashley and rime3-14.
