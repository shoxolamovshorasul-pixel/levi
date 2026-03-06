
import asyncio
from aiogram import Bot, Dispatcher, F
from aiogram.types import Message, ReplyKeyboardMarkup, KeyboardButton
from aiogram.filters import CommandStart

TOKEN = "8621370689:AAFoaRucnPTRK838fPd758hOc6P-a0UmbpE"

bot = Bot(token=TOKEN)
dp = Dispatcher()


menu_keyboard = ReplyKeyboardMarkup(
    keyboard=[
        [KeyboardButton(text="O'zbek Tili")],
        [KeyboardButton(text="Ingiliz Tili")],
    ],
    resize_keyboard=True
)

option_kb = ReplyKeyboardMarkup(
    keyboard=[
        [KeyboardButton(text="SET 1"), KeyboardButton(text="SET 2")],
        [KeyboardButton(text="Back")]
    ],
    resize_keyboard=True
)


set1_menu = ReplyKeyboardMarkup(
    keyboard=[
        [KeyboardButton(text="Tvister kombo")],
        [KeyboardButton(text="Back")]
    ],
    resize_keyboard=True
)


set2_menu = ReplyKeyboardMarkup(
    keyboard=[
        [KeyboardButton(text="Chizburger kombo")],
        [KeyboardButton(text="Back")]
    ],
    resize_keyboard=True
)


@dp.message(CommandStart())
async def start_handler(message: Message):
    await message.answer("Salom! Tilni tanlang", reply_markup=menu_keyboard)


@dp.message(F.text == "O'zbek Tili")
async def uzbek_handler(message: Message):
    await message.answer("Menyuni tanlang", reply_markup=option_kb)


@dp.message(F.text == "SET 1")
async def set1_handler(message: Message):
    await message.answer("SET 1 menyusi", reply_markup=set1_menu)

@dp.message(F.text == "Tvister kombo")
async def tvister_handler(message: Message):
    photo = "https://kfc.com.uz/admin/files/5823.jpg"
    await message.answer_photo(
        photo=photo,
        caption="Tvister kombo — 36 000 so'm",
        reply_markup=option_kb 
    )

@dp.message(F.text == "SET 2")
async def set2_handler(message: Message):
    await message.answer("SET 2 menyusi", reply_markup=set2_menu)


@dp.message(F.text == "Chizburger kombo")
async def chizburger_handler(message: Message):
    photo = "https://kfc.com.uz/admin/files/5826.jpg"
    await message.answer_photo(
        photo=photo,
        caption="Chizburger kombo — 32 000 so'm",
        reply_markup=option_kb  
    )


@dp.message(F.text == "Back")
async def back_handler(message: Message):
    await message.answer("Bosh menyu", reply_markup=menu_keyboard)

async def main():
    print("Bot ishladi...")
    await dp.start_polling(bot)

if __name__ == "__main__":
    asyncio.run(main())
