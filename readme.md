
**Birthday Email Generator**

- **Description:**: A small Python project that builds a polished HTML birthday email from a plain-text template and (optionally) sends it via SMTP. The repository generates the card-style email shown in the screenshot (`image.png`) — a gradient header with emojis, a large personalized title (e.g. "Happy Birthday, Teejay!"), and a clean, readable body with paragraph spacing and a footer.

**Preview:**
- **Screenshot:**: See [image.png](image.png) for a sample output captured in an email client.

**What It Does**
- **Template:**: Reads `Data/Birthday_Wish_Template.txt` and replaces placeholders like `{name}` and `[Your Name]` with actual values.
- **HTML Builder:**: `build_html.build_birthday_email()` wraps the personalized text into a responsive, card-style HTML email with a banner, body paragraphs, decorative divider, and footer.
- **Sender:**: `send.send_birthday_email()` sends the HTML email via SMTP (defaults to Gmail SMTP settings).

**Quick Start**
- **1) Install dependencies:**

```bash
pip install python-dotenv
```

- **2) Add credentials:** Create a `.env` file in the project root with your sending address and password (use an App Password for Gmail):

```text
my_email=you@example.com
my_password=your_app_password
```

- **3) Edit the message:** Customize `Data/Birthday_Wish_Template.txt` to change wording and placeholders.

- **4) Run the example:**

```bash
python app.py
```

Note: `app.py` builds the message for `Teejay` and then calls the sender function. Modify `app.py` or call `build_birthday_email()` directly to preview without sending.

**Preview HTML (optional)**
- To preview the generated HTML locally without sending, run a short Python snippet to write output to `preview.html` and open it in your browser.

```bash
python - <<'PY'
from build_html import build_birthday_email
from utils import read_file, modify
content = modify(read_file('Data/Birthday_Wish_Template.txt'), 'Teejay', 'Taofeek')
html = build_birthday_email(name='Teejay', body_text=content, sender_name='Taofeek')
open('preview.html','w',encoding='utf-8').write(html)
print('Wrote preview.html')
PY
```

**Files You Care About**
- **`app.py`**: Example runner that builds and sends the email ([app.py](app.py)).
- **`build_html.py`**: Produces the HTML email body ([build_html.py](build_html.py)).
- **`send.py`**: Sends email via SMTP ([send.py](send.py)).
- **`utils.py`**: Helpers to read/modify the template and load `.env` ([utils.py](utils.py)).
- **`Data/Birthday_Wish_Template.txt`**: The message template used for personalization ([Data/Birthday_Wish_Template.txt](Data/Birthday_Wish_Template.txt)).

**Security & Notes**
- **Use App Passwords:** For Gmail, create an App Password rather than using your main account password.
- **Do not commit secrets:** Add `.env` to `.gitignore` and never commit real credentials.
- **Compatibility:** The generated HTML is simple and compatible with most email clients; test in your target clients before wide sending.

**Next Steps / Customization Ideas**
- Swap templates per occasion or support CSV-based personalization using `Data/products.csv` as inspiration for data-driven messages.
- Add an option to save outbound HTML files rather than sending immediately for preview workflows.

If you want, I can open `preview.html` for you, add a small preview command to `app.py`, or create a `requirements.txt` to pin dependencies.
