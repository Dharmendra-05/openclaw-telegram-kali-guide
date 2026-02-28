How to Create Your Own Telegram Bot Using OpenClaw on Kali Linux (VirtualBox)

Welcome! This guide will walk you through the entire process of setting up OpenClaw—a powerful personal AI agent—on a Kali Linux virtual machine to power your very own Telegram bot.

By the end of this tutorial, you will have a functional AI assistant that can run commands and perform automation tasks directly from your phone.

🛠 Prerequisites

Before we begin, ensure you have the following:

VirtualBox installed: Download it here.

Kali Linux ISO or OVA: Download from Kali.org.

A Google Account: Ensure 2-Factor Authentication (2FA) is enabled (required for Google Cloud/AI Studio projects).

A Telegram Account: To create and interact with your bot.

[!WARNING]
Security First: OpenClaw requires administrator rights for automation. Using Kali Linux inside VirtualBox provides a safe, isolated environment. Never share your API keys or Bot Tokens with anyone.

🚀 Step 1: Setting up the Virtual Machine

Create VM: Open VirtualBox and create a new VM for Kali Linux.

Memory/CPU: Assign at least 4GB of RAM and 2 CPU cores for a smooth experience.

Login: The default credentials for Kali are:

Username: kali

Password: kali

Change Password: Open the terminal and type passwd to change your password immediately.

📦 Step 2: System Update & Tool Installation

Open your Kali terminal and run these commands to prepare your environment:

1. Update the System

sudo apt update && sudo apt upgrade -y


2. Install Node.js, Git, and Build Tools

sudo apt install -y nodejs git build-essential procps curl file


3. Install pnpm (OpenClaw's preferred package manager)

sudo npm install -g pnpm


🏗 Step 3: Installing OpenClaw

You have two ways to install OpenClaw. The Docker method is recommended for better stability.

Option A: Native Installation (Manual)

git clone [https://github.com/openclaw/openclaw.git](https://github.com/openclaw/openclaw.git)
cd openclaw
pnpm install
pnpm ui:build
pnpm build
pnpm link --global
openclaw onboard --install-daemon


Option B: Docker Method (Recommended)

git clone [https://github.com/openclaw/openclaw.git](https://github.com/openclaw/openclaw.git)
cd openclaw
./docker-setup.sh
docker compose run --rm openclaw-cli status


🍺 Step 4: Installing Homebrew (Dependencies)

OpenClaw may require Homebrew to manage certain internal skills and packages.

/bin/bash -c "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"

# Add Homebrew to your path
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> $HOME/.zshrc
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

# Verify installation
brew doctor


If successful, you should see: "Your system is ready to brew."

🔑 Step 5: Obtaining Your API Keys

1. Gemini AI API Key

Go to Google AI Studio.

Create a new project (requires 2FA).

Generate an API Key. (This guide uses the Gemini 2.5 Flash free tier).

Copy this key; you will need it for the OpenClaw configuration.

2. Telegram Bot Token

Search for @BotFather on Telegram.

Send the command /newbot.

Follow the prompts to name your bot (e.g., MyKaliBot).

BotFather will give you an Access Token. Keep this safe!

⚙️ Step 6: Configuring OpenClaw & Pairing

Now, let's link everything together.

Start OpenClaw: If using the native install, run openclaw. You will be prompted to enter your Gemini API Key.

Onboard the Bot:

clawdbot onboard


Select Telegram from the list of channels and paste your Bot Token from BotFather.

Pairing the Bot:

Open your new bot in Telegram and send /start.

The bot will reply with a Pairing Code.

Back in your Kali terminal, run:

openclaw pairing approve telegram [YOUR_CODE_HERE]


🧪 Step 7: Final Testing

Once paired, your bot is alive! Try sending a message to your bot on Telegram:

Hello!

What is the current system load?

OpenClaw will process these via the Gemini model and respond directly in your chat.

🛠 Troubleshooting

Command Not Found: If openclaw doesn't work, try pnpm exec openclaw.

API Rate Limits: If you see "API rate limit reached," wait a few minutes. The free tier of Gemini has usage limits.

Docker Issues: Ensure your user is part of the docker group: sudo usermod -aG docker $USER and restart.

📜 Credits & Security Warning

OpenClaw is a personal agent. It can read files and run actions. Ensure you read the Security Guidelines before exposing it to the internet.

Happy Hacking!
