# micro-allinone2

This project is a microservice that uses a GitHub Action to create dated markdown files. The service is triggered by a POST request to the `/api/trigger-action` endpoint.

## How it Works

1.  A POST request is sent to `/api/trigger-action`.
2.  The `api/trigger-action.js` script receives the request and triggers a `repository_dispatch` event on GitHub.
3.  The `.github/workflows/create-file.yml` GitHub Action is triggered by the `repository_dispatch` event.
4.  The action creates a new markdown file in the `contents` directory with the current date and time as the filename.

## Troubleshooting

We recently encountered an issue where the markdown files were being created with the correct filename, but were empty of content. This was due to a typo in the `event_type` in `api/trigger-action.js`. The script was sending `create-dated-.file` instead of `create-dated-file`, which caused the GitHub Action to not receive the content payload.

The issue was resolved by correcting the typo in `api/trigger-action.js`.

## Running Locally

To run the service locally, you can use the following command:

```bash
source myenv/bin/activate && FLASK_APP=api/index.py flask run &
