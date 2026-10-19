# Login on TV

TV apps move the login to a phone or computer. The TV only waits for the result.

## How it works

| Step | Who | What happens |
| ---- | --- | ------------ |
| 1 | TV | Asks the backend for a device code and a short user code |
| 2 | TV | Shows the user code, a short URL, and a QR code. The QR code encodes the URL with the code already filled in |
| 3 | User | Scans the QR code, or opens the URL and types the code |
| 4 | User | Logs in on the phone, using a saved password or biometrics |
| 5 | TV | Polls the backend every few seconds: "has this code been approved yet?" |
| 6 | TV | Once approved, the poll returns tokens. The TV stores them and moves to the Home screen |

## Details that matter on TV

| Topic | Problem | Solution |
| ----- | ------- | -------- |
| Focus | The page has no natural focusable element, so the D-pad does nothing | Give the "Get a new code" button initial focus |
| Expiry | Codes expire | Refresh automatically, or show an expired state with a focusable retry |
| Readable code | Codes are read from across a room | Use large type, high contrast, and no confusable characters |
| Back button | Back could leave the login screen running in the background | Back leaves the login screen and stops polling |

## Rules

- Stop polling as soon as the user leaves the login screen or the code is approved.
- Every expired code must lead to a focusable action.
