# python_training_mantis — end-to-end tests for MantisBT

Automated tests for the **Mantis Bug Tracker** combining the web UI, the SOAP API, a mail server and FTP-based environment setup.

## What is tested

- **Login** through the UI
- **Projects**: create and delete through the UI, then verify the result through the **SOAP API** (UI action, API check)
- **User sign-up end to end**: create a mailbox on the James mail server, register in Mantis, read the confirmation email via POP3, follow the link and check the new account can log in through the API

## Stack

| | |
|---|---|
| UI automation | Selenium WebDriver |
| Test runner | PyTest (fixtures, data-driven tests from JSON) |
| API | SOAP (suds client, `mantisconnect.php`) |
| Email | Apache James (telnet admin), POP3 |
| Environment | Server config pushed and restored over FTP (ftputil) before and after the run |

## Run it

Requires a local MantisBT and James mail server; set URLs and credentials in `target.json`.

```bash
pip install selenium pytest jsonpickle suds-py3 ftputil
pytest test/ --browser=chrome
```
