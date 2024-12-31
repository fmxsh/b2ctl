# b2ctl - Backblaze B2 Command-Line Utility

This script provides a command-line interface for managing files in a Backblaze B2 bucket. It allows users to list, upload, download, and delete files, as well as interact with the B2 bucket in an interactive mode.

> [!NOTE]
> This script is made for use with Bucket keys not the master key. Create a bucket and create an application key for the bucket. Get the KeyID and the secret APP_KEY that was generated and showed once.

> [!NOTE]
> We do not need bucketName, as it is derived from the KeyID which is tied to the bucket.

## Prerequisites

- A Backblaze B2 account with an application key.
- `curl` installed on your system.

## Setup

1. Set the required environment variables for your B2 account credentials:

   ```bash
   export B2CTL_KEY_ID="your_account_key_id"
   export B2CTL_APP_KEY="your_application_key"
   ```

2. Ensure the script has execution permissions:
   ```bash
   chmod +x script.sh
   ```

## Usage

Run the script with one of the following options:

### Interactive Mode

Start an interactive session:

```bash
./script.sh --interactive
```

### List Files

List all files in the bucket:

```bash
./script.sh --list
```

### Upload File

Upload a file to the bucket:

```bash
./script.sh --up <source_file_path>
```

### Download File

Download a file from the bucket:

```bash
./script.sh --down <file_name> <destination_directory>
```

### Delete File

Delete a file from the bucket interactively or by file name (using `--interactive` mode or extending the script).

## Notes

- Make sure the script is authorized with valid credentials.
- The `--interactive` mode allows file selection and actions like listing, downloading, and deleting files interactively.

## Troubleshooting

- If authorization fails, verify that the environment variables `B2CTL_KEY_ID` and `B2CTL_APP_KEY` are correctly set.
- Ensure network connectivity to Backblaze B2 endpoints.
