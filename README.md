# b2ctl - Backblaze B2 Command-Line Utility

This script provides a command-line interface for managing files in a Backblaze B2 bucket. It allows users to list, upload, download, and delete files, as well as interact with the B2 bucket in an interactive mode.

> [!NOTE]
> This script is made for use with Bucket keys not the master key. Create a bucket and create an application key for the bucket. Get the KeyID and the secret AppKey that was generated and showed once.

> [!NOTE]
> We do not need bucketName or bucketID, as it is derived from the KeyID which is tied to the bucket.

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
   chmod +x b2ctl
   ```

## Usage

Run the script with one of the following options:

### Select mode and target file descriptor

For select mode, you can invoke the script with `--fd 10` and it will write the selected filename to file descriptor 10 and quit (assuming a caller script is ready to recieve it like:

```bash
./b2ctl --fd 10 10> >(while read -r line; do
	echo "Captured output: $line"
done)
```

#### Setting the destination directory for downloaded file

The file that is selected will be downloaded into the directory specified by `--dest`.

```bash
./b2ctl --dest <destination_directory> --fd 10
```

### Interactive Mode

Start an interactive session:

Either start `b2ctl` without any arguments, or use the `--interactive` flag:

```bash
./b2ctl

# or

./b2ctl --interactive
```

### List Files

List all files in the bucket:

```bash
./b2ctl --list
```

### Upload File

Upload a file to the bucket. It will be named same in bucket as it is name at source.

```bash
./b2ctl --up <source_file_path>
```

Supports piped data.

In such case <source_file_path> doesn't have to exist as a file where the script is running. The filename is used as the name for the desitnation file in the bucket. Thus it becomes <dest_file_name>.

```bash
echo "my data" | ./b2ctl --up <dest_file_name>
```

### Download File

Download a file from the bucket:

```bash
./b2ctl --down <file_name> <destination_directory>
```

### Delete File

Delete a file from the bucket interactively or by file name (using `--interactive` mode or extending the script).

## Notes

- Make sure the script is authorized with valid credentials.
- The `--interactive` mode allows file selection and actions like listing, downloading, and deleting files interactively.

## Troubleshooting

- If authorization fails, verify that the environment variables `B2CTL_KEY_ID` and `B2CTL_APP_KEY` are correctly set.
- Ensure network connectivity to Backblaze B2 endpoints.
