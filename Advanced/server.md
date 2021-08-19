# 📖 The Reason for Using a Server

Virtual servers are running in server rooms with a way more stable condition and usually faster Internet connection speed. You can also run the job and forget about it / prevent the job being interupted by your own expected moves.

# 🎬 Enviroment Preparation

![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white) ![Apple](https://img.shields.io/badge/macOS-000000?style=for-the-badge&logo=apple&logoColor=white)

I'm running the jobs on [Amazon Lightsail](https://lightsail.aws.amazon.com/), using Ubuntu 20.04 LTS.

```bash
sudo apt update
sudo apt upgrade -y
```

Install the required components

```bash
sudo apt install python3 python3-pip python-is-python3 ffmpeg atomicparsley
pip install --upgrade youtube-dl
pip install --upgrade streamlink
```

For ffmpeg, it might require a higher version to deal with vp9 video/audio muxing, read [this article](https://ubuntuhandbook.org/index.php/2021/05/install-ffmpeg-4-4-ppa-ubuntu-20-04-21-04/) to find out how to install ffmpeg 4.4 or higher.

# Usage

## 🚩 youtube-dl

Should be the mostly used tool to download youtube-dl videos, as well as the generic `.m3u8`. Simple as it is.

```bash
youtube-dl "url"
```

<details>
  <summary>Configuration example</summary>
  
  ```bash

  -o '/home/ubuntu/raw/(upload_date)s %(title)s.%(ext)s'

  --embed-thumbnail

  --format 'bestvideo+bestaudio/best/mp4'

  --merge-output-format mp4

  --add-metadata

  --cookies '/home/ubuntu/cookies.txt'
  ```

  ※ Replace `/home/ubuntu/` and `/home/ubuntu/raw` with your own working directories.

  Save it as `youtube-dl.conf` in e.g. `/home/ubuntu/youtube-dl.conf`. Then use `sudo cp youtube-dl /etc/youtube-dl.conf` to make it a system-wide config.
  
</details>

<br>

Putting a `--cookies cookies.txt` option helps downloading the member-only contents.

To get a `cookies.txt` using the plugin: [[Chrome](https://chrome.google.com/webstore/detail/get-cookiestxt/bgaddhkoddajcdgocldbbfleckgcbcid)] [[Firefox](https://addons.mozilla.org/en-US/firefox/addon/cookies-txt/)]

Also, the config takes 3 times of writing files which might take longer. *Wait patiently.*

> Downloaded video and audio → Merged .mp4 file → Write metadata → Write thumbnail with AtomicParsley

## 🚩 streamlink

For **No Archive** streams youtube-dl doesn't work. We should use streamlink instead.

```bash
streamlink "url" best -o "filename.ts" # Name the filename as .ts, not .mp4
```

Streamlink works for niconico with options provided.

```bash
streamlink "url" best --niconico-email "EMAIL" --niconico-password "PASSWORD" -o "filename.ts"
```

For AbemaTV, streamlink also works. But somehow it's a little bit slow. You can also use `yuu` instead [[Github](https://github.com/noaione/yuu)].

## 🚩 minyami

This is so far the best and fastest way to archive niconico timeshift.

The whole preparation starts from installing the `node.js` environment.

I strongly recommend using `tj/n` instead of `nvm`, also don't install `npm` with `apt-get` to avoid permission problems.

### 1. Install `tj/n` and `Node.js`

On most Linux / macOS machines, this should be able to install with the script

```bash
curl -L https://git.io/n-install | bash
```

Once it's installed, type `n lts` to install the latest lts version of Node.js.

Check the original repo for more info: [`tj/n`](https://github.com/tj/n)

### 2. Extention

This tool requires a Chrome extension to extract playback address and key to download the whole archive.

Download the [Chrome extension](https://chrome.google.com/webstore/detail/minyami/cgejkofhdaffiifhcohjdbbheldkiaed) from the Chrome store, or build the extension from source [here](https://github.com/Last-Order/Minyami-chrome-extension).

### 3. Usage

Go to a playback page, start the playback and drag the progress bar to somewhere near the middle to avoid extracting a bad link.

Click the extenstion and extract the command, then paste it in your shell.

This should be able to download fluently, no extra cookies are required.

### 4. Warning

During the test, I found some IP of the IDC (e.g aws) might have been banned and ran into some problems.

You might see bunches of 403 error during download. The reason is unknown.

So be careful using this tool.
