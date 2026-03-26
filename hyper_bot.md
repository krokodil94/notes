# hyper_bot

  Useful commands to manage it:

  # View live logs

  

  # Check status
  ssh -i "..." ubuntu@92.4.173.164 "docker ps --filter name=hyper_bot"

  # Stop bot
  ssh -i "..." ubuntu@92.4.173.164 "docker stop hyper_bot"

  # Restart after config change
  ssh -i "..." ubuntu@92.4.173.164 "docker stop hyper_bot && docker rm hyper_bot && docker build -t
  hyper_bot:latest /home/ubuntu/hyper_bot && docker run -d --name hyper_bot --restart unless-stopped
  -v /home/ubuntu/hyper_bot/hyper_bot.log:/app/hyper_bot.log hyper_bot:latest"

  The bot is:
  - Running in a container with --restart unless-stopped — survives server reboots
  - Logs persist at /home/ubuntu/hyper_bot/hyper_bot.log on the host
  - Running LIVE (DRY_RUN=False), 6x leverage, BTC only