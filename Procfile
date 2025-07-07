from aiogram import Bot, Dispatcher, types
from aiogram.utils import executor
import yt_dlp
import os

API_TOKEN = os.getenv("7539658089:AAGwBPqeyn_TQOk5UGkcrh3bm4VcOfVsRA0")
bot = Bot(token=API_TOKEN)
dp = Dispatcher(bot)

@dp.message_handler()
async def download_video(message: types.Message):
    url = message.text
    if any(domain in url for domain in ["youtu", "tiktok", "instagram"]):
        await message.reply("⏳ Yuklab olinmoqda...")

        try:
            ydl_opts = {
                'format': 'best',
                'outtmpl': 'video.%(ext)s',
                'noplaylist': True,
            }

            with yt_dlp.YoutubeDL(ydl_opts) as ydl:
                info = ydl.extract_info(url, download=True)
                filename = ydl.prepare_filename(info)

            if os.path.exists(filename):
                with open(filename, 'rb') as video:
                    await bot.send_video(message.chat.id, video)
                os.remove(filename)
            else:
                await message.reply("❌ Video topilmadi.")
        except Exception as e:
            await message.reply(f"❌ Xatolik yuz berdi: {e}")
    else:
        await message.reply("Faqat YouTube, TikTok yoki Instagram link yuboring.")

if __name__ == '__main__':
    executor.start_polling(dp)
