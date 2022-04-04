# queuecounter.py
# Count items in your reports and modqueues

import praw
import time
from datetime import datetime as dt


sub_name = input("Please enter the subreddit name...\n> ")

def login():
	reddit = praw.Reddit(
      	user_agent = 'Reports Queue Counter Bot v.01 by u/BuckRowdy',
      	client_id = '',
      	client_secret = '',
      	refresh_token = ''
  )
	return reddit

def how_many_items(subreddit):
    modqueue_count = len(list(subreddit.mod.modqueue(limit=None)))
    reported_items = len(list(subreddit.mod.reports(limit=None)))
    time_stamp = dt.fromtimestamp(int(time.time())).strftime('%a, %B %d, %Y at %H:%M:%S')
    print(f'\n\n{time_stamp}')
    print('--- Items Remaining in Queue ---')
    print(f'> Subreddit:\tr/{subreddit}')
    print(f'> Reports:\t{reported_items}')
    print(f'> Modqueue:\t{modqueue_count}')
    print('--------------------------------')
    
######################################

if __name__ == "__main__":
 
  reddit = login()
  subreddit = reddit.subreddit(sub_name)
  how_many_items(subreddit)


