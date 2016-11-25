# s3-cloud

Poor man's cloud, backed on S3.

This tool allows to synchronize, manage and share files on an S3 bucket as well
as render Markdown documents as PDF files for administrative communication.

It uses `s3cmd` for all AWS API calls (it is intended as a convenience tool,
not a breakthrough in any way). It is expected `s3cmd` has been configured
first.

Below, the notion of *endpoint* is defined as an S3 URL; it translates to a
local path as follows for swift handling:

- `s3://my-bucket/documents`: `~/Documents`

## Commands

- push
- pull
- sync
- delete
- share
- render

### `push` command

Push objects to an S3 endpoint.

Options:

- `-d`, `--delete`: allow object deletion

Sample usage:

    s3-cloud push s3://my-bucket/documents

### `pull` command

Pull objects from an S3 endpoint.

Options:

- `-d`, `--delete`: allow object deletion

Sample usage:

    s3-cloud pull s3://my-bucket/documents

### `sync` command

Synchronize objects with an S3 endpoint (pull and push).

Options:

- `-d`, `--delete`: allow object deletion

Sample usage:

    s3-cloud sync s3://my-bucket/documents

### `delete` command

Delete an object on an S3 bucket.

Sample usage:

    s3-cloud delete s3://my-bucket/documents/test.pdf

### `share` command

Generate a sharing link for an S3 object.

Options:

- `-e`, `--expire`: set link expiry time, eg. 7d

Sample usage:

    s3-cloud share s3://my-bucket/documents/test.pdf -e 7d

### `render` command

Render a Markdown file as a PDF.

Options:

- `-p`, `--preview`: automatically preview document
- `-s`, `--css`: CSS stylesheet
- `-f`, `--format`: paper format, eg. A4 (default)
- `-m`, `--margins`: paper margins, eg. 2cm (default)
- `-o`, `--orientation`: document orientation

Sample usage:

    s3-cloud render s3://my-bucket/documents/test.md -p

Markdown rendering supports custom classes through annotations (eg. `{right}`);
here are some classes defined in the default CSS:

- `right`: align a block of text on the right-half of the page
- `letter-indent`: add 3em worth of indentation for the first line in
  paragraphs
- `t-2` to `t-10`: add 2 to 10 em worth of top margin
- `b-2` to `b-10`: add 2 to 10 em worth of bottom margin
- `signature`: limit an image's width to 10em

It also contains rules for links, code, citations, tables and horizontal rules.
