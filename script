import hashlib
import requests
import json
from sys import argv


def sha256(str):
    return hashlib.sha256(str.encode('utf-8')).hexdigest()


def sign_gen(a,b):
    step1= f"leaderboard{120}{a ^ b}ping"
    step2 = sha256(step1)
    return sha256(step2+'catalog')


USER_ID = argv[0]
AUTH_ID = argv[1]
URL_START = 'https://beeline-uppers.ru-prod2.kts.studio/api/game/start'
URL_FINISH = 'https://beeline-uppers.ru-prod2.kts.studio/api/game/finish'
AUTH = {'Authorization':f'Bearer {AUTH_ID}'}


while True:
    start = requests.post(URL_START, headers=AUTH)
    gameid = start.json()['data']['id']
    req = json.loads('{"id":%s,"victory":false,"coins":120,"tutorial":false,"sign":"%s"}'%(gameid,sign_gen(USER_ID, gameid)))
    finish = requests.post(URL_FINISH, json=req, headers=AUTH)
