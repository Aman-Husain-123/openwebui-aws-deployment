<<<<<<< HEAD
# openwebui-aws-deployment
=======
# ChatGPT (Open WebUI) — EC2 Deployment and Monitoring

Overview
- This project hosts an Open WebUI (ChatGPT-like) instance on an Amazon EC2 instance and exposes it for users to register and use available models. Grafana + OTEL are used for monitoring.

Screenshots
- Home / prompt page
  ![Open WebUI Home](docs/screenshots/open-webui-home.png)
- Chat / conversation view
  ![Open WebUI Chat](docs/screenshots/open-webui-chat.png)
- Grafana monitoring dashboard
  ![Grafana Dashboard](docs/screenshots/grafana-dashboard.png)
- EC2 terminal showing Docker / containers
  ![EC2 Docker Terminal](docs/screenshots/docker-terminal.png)

(Place the screenshots you provided into `docs/screenshots/` with the filenames above so they display.)

Repository layout (important files)
- `aman_euri_new.ppk` — SSH key (PuTTY) for connecting if applicable
- `open_webui_monitoring_json_9SsY.json` — Grafana dashboard JSON or config
- `Openwebui_ec2_setup_and_monitoring_docx_gm4U.docx` — detailed setup notes (reference)

Prerequisites
- AWS EC2 instance (Ubuntu recommended)
- Security group: allow inbound TCP for ports 8000 (Open WebUI), 3000 (Grafana), and other OTEL ports as needed (4317/4318) — restrict by IP where possible
- Docker Engine and Docker Compose (v2)

Quick deployment (on EC2 Ubuntu)
1. SSH into instance (example using OpenSSH):
   ssh -i "path/to/key.pem" ubuntu@<EC2_PUBLIC_IP>

2. Clone or copy project files to the instance.

3. Start containers (example of your compose file name):
   sudo docker compose -f docker-compose.otel.yaml up -d

4. Verify running containers:
   docker ps

If you get permission denied for the Docker socket:
- Add the ubuntu user to the docker group and re-login / refresh groups:
  sudo usermod -aG docker ubuntu
  newgrp docker
  docker ps

Notes for Windows (PowerShell) users
- If you need to SCP or upload files from Windows PowerShell, use scp (when using OpenSSH) or a tool like WinSCP / PuTTY for PPK keys.
- Example scp (PowerShell):
  scp -i "C:\path\to\key.pem" .\open_webui_monitoring_json_9SsY.json ubuntu@<EC2_PUBLIC_IP>:/home/ubuntu/

Access URLs
- Open WebUI (example): http://<EC2_PUBLIC_IP>:8000
- Grafana: http://<EC2_PUBLIC_IP>:3000

User registration and models
- The Open WebUI instance supports user registration (if enabled in your config). Follow the UI registration flow or consult `Openwebui_ec2_setup_and_monitoring_docx_gm4U.docx` for specific application settings and authentication provider details.

Grafana and OTEL
- Grafana is bundled (or run separately). Import `open_webui_monitoring_json_9SsY.json` if needed or use the provided dashboard in `docs/`.
- Ensure OTEL collector ports are reachable from the application containers (4317/4318) and that Grafana can read the telemetry backend.

Troubleshooting
- Docker permission errors: see usermod step above
- Missing images in README: make sure to place screenshots in `docs/screenshots/` using the filenames in the Screenshots section
- Containers not binding: confirm security group rules and that no other service uses the same ports

Useful commands
- Start (detached): sudo docker compose -f docker-compose.otel.yaml up -d
- Stop: sudo docker compose -f docker-compose.otel.yaml down
- Show containers: docker ps --format "table {{.ID}}\t{{.Image}}\t{{.Status}}\t{{.Ports}}"
- Show logs (example): docker logs -f open-webui

Contact / Next steps
- If you want, I can: update this README with exact variable names from your compose files, embed the actual dashboard JSON, or add a step-by-step sequence for creating the EC2 AMI and automating deployment.

--
Saved screenshots path reminder: docs/screenshots/open-webui-home.png, docs/screenshots/open-webui-chat.png, docs/screenshots/grafana-dashboard.png, docs/screenshots/docker-terminal.png
>>>>>>> 87013e5 (Add Chatgpt deployment files (Open WebUI, Grafana dashboard, docs))
