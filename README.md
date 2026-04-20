# Certifie

A **Django web app for bulk certificate generation**. Upload an Excel file with recipient names and details, select a certificate template, and Certifie generates a personalised image for each row - then emails the whole batch to you as a ZIP file. Generated images are deleted from the server immediately after sending.

---

## How It Works

1. **Log in** with your account (Google OAuth via `django-allauth` supported)
2. **Browse** the certificate template library
3. **Upload** an Excel file with recipient data (name, details, etc.)
4. Certifie uses **Pillow** to render each name and field onto the template, respecting per-template font, size, and bounding box coordinates
5. All generated PNGs are zipped and **emailed to your account address** via SMTP
6. Generated files are **wiped from the server** after sending - nothing is stored

---

## Features

- Bulk certificate generation from Excel (`.xlsx`) input
- Up to 3 signature variants per certificate template
- Per-template configurable font, font size, and text bounding boxes
- Automatic ZIP packaging and email delivery
- Login-gated - all routes require authentication
- Zero data retention - generated images deleted post-send

---

## Tech

- **Framework:** Django 3.x
- **Image processing:** Pillow (PIL)
- **Data input:** pandas (Excel parsing)
- **Auth:** Django auth + `django-allauth` (Google OAuth)
- **Email:** SMTP via Gmail
- **Database:** SQLite (dev) / Heroku Postgres (prod)
- **Deployment:** Heroku (`Procfile` + `runtime.txt`)

---

## Local Setup

```bash
git clone https://github.com/Raffiesaurus/Certifie.git
cd Certifie
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Then visit `http://localhost:8000/` and log in with your superuser credentials.

To add certificate templates, go to `/admin/` and create `certificate` and `font` objects.

---

## Excel Format

Each row in the uploaded `.xlsx` file represents one recipient. Columns map to the text fields defined in the certificate template's bounding box configuration (name, subtitle, extra fields).

---

## Project Structure
```
Certifie/             # Django project settings, URLs
certificates/         # Main app - models, views, forms, templates
Generated_Images/     # Temp output directory (cleared after each run)
static/               # Static assets
certificates/         # Certificate template images (stored via media)
```

---

## License

MIT
