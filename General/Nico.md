## 🔨 Tool Preparation

|Tool|Description|Download|
|:--:|:--:|:--:|
|streamlink|Live stream recording tool|[Github](https://github.com/streamlink/streamlink)
|minyami|Niconico timeshift downloader|[Github](https://github.com/Last-Order/Minyami)|
|ffmpeg|Fundemental media processor|[Github](https://github.com/FFmpeg/FFmpeg)|
|Stream Recorder|Stream recording extension|[Chrome Store](https://chrome.google.com/webstore/detail/stream-recorder-download/iogidnfllpdhagebkblkgbfijkbkjdmm)|

## 🎪 Windows Environment Preparation

![Windows 10](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)

**※ If you are working on a headless server like I do, please read the [advanced guide](/Advanced/server.md)**

**※ If you don't want to do the configuration yourself, you can use the scripts provided [here](/scripts)**

First of all, you should setup a `PATH` folder to tell the Windows where to find the programs.

Run Command Prompt (cmd) as administrator. Then paste the following into the console

```powershell
setx /M PATH "%PATH%;<REPLACE THIS WITH THE PATH TO YOUR DIRECTORY>"
```
The `REPLACE THIS WITH THE PATH TO YOUR DIRECTORY` part should be the folder want to save the tools. In [this case](/assets/dir1.PNG) it sould be `J:\Youtube Downloading`.

Once you are done, put the tools in the folder. Start cmd (doesn't not have to be as administrator) and run the commands `youtube-dl --help` or `streamlink -h` etc. If you see a giant block of text showing you the arguments, that means it's working.

Tips: 

> If you are not sure about how to download things on Github, just check the `releases` on the right of the page.
>
> Select the .exe file or the package having "windows" or "amd64" in it.

Another alternative way to install these are by using `pip3`. Just install `python` [link](https://www.python.org/) and type `pip3 install youtube-dl` and `pip3 install streamlink`.

## Usage

### 🚩 streamlink

**※ If you don't want to do the configure yourself, you can use the scripts provided [here](/scripts)**

Streamlink is possibly the best and the most stable way to record Niconico streams.

```powershell
streamlink "url" best --niconico-email "EMAIL" --niconico-password "PASSWORD" -o "filename.ts"
```

Notice:

1. **DO NOT** open the same streaming page once you started the recording, it will broke the record session
2. You **MUST** put the `--niconico-email` and `--niconico-password` before `-o` or it won't work
3. I personally don't suggest recording the Niconico stream during live, the network might broke up when switching from free to paid corner

If you don't want to type your `EMAIL` and `PASSWORD` here, you can use `--niconico-user-session` instead. You can extract the cookies by using `cookies.txt` plugin.

### 🚩 Minyami

This is a project working pretty efficently in Niconico Timeshift (stream archive) downloading.

You don't have to wait for hours when downloading the archive.

#### Installation
First, you have to install a `Node.js` environment.

For Windows, download `Node.js` installer from the [official page](https://nodejs.org/en/download/), Linux please follow the advanced guide.

Once you are done with installing, type `npm -v` to see if `npm` is functioning properly.

Type `npm i -g minyami` to install `minyami`.

Type `minyami version` to see if minyami installed. Should return messages like this

```
Minyami / A lovely video downloader / 4.2.7
うめにゃん~ (虎>ω<)
```

Then install the [chrome extension](https://chrome.google.com/webstore/detail/minyami/cgejkofhdaffiifhcohjdbbheldkiaed) for link and playback key extraction.

#### Usage

Go to niconico timeshift playback page, drag the progress bar to somewhere in the middle, then use the extension to extract the link.

Paste the link into the CLI interface and download.

#### Caution

During the test, I found some IP of the IDC (aws) might have been banned and ran into some problems.

You might see bunches of 403 error during download. The reason is unknown.

So be careful using this tool.

### 🚩 Stream Recorder

This is a plugin which can directly grab the stream. It did a great job in the **SUISEI "POWER" LIVE**. I successfully saved the live-record edition using this plugin.

The details were written in the plugin, **read before use**, *the plugin does not support encrypted HLS stream*. You might have to refresh and grab for several times until you see the higher resolution. 

> Be careful, don't refresh the streaming page or the recording session will interupt.

And it does not work with `YouTube`, so you still need `streamlink`.
