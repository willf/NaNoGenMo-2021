# NaNoGenMo 2021 Entry
## Will Fitzgerald

## Brainstorming Movies

**First of all: [The Results](nanogenmo2021.md)**

<img src="https://upload.wikimedia.org/wikipedia/commons/1/1f/The_Pleasure_Seekers_%281920%29_-_4.jpg"  width="200" />

Here's the basic idea:

1. Get a big list of movie names, say, from [American films from 1920](https://en.wikipedia.org/wiki/List_of_American_films_of_1920)
2. Generate a prompt from this information to send to OpenAI's generate API.
3. Turn this all into a story.

Most of the code here is about managing text. Basically, things go through these stages:

1. First a [text file](table.txt) was created from [Wikipedia](https://en.wikipedia.org/wiki/List_of_American_films_of_1920). This was done manaually.
2. Then this is parsed, and a [JSONL-format](https://jsonlines.org) file is created, with parsed information, one per line: [table.json](table.json).
3. Then, this is enriched by creating a prompt which is sent to the Open API and then collecting the result and adding it to the dictionaries, again, one per line: [synopsis.json](synopsis.json).
4. Then, a script is run to create the result, which is called [Possible Movies](nanogenmo2021.md).

```bash
❯ python nanogenmo2021.py --help              
usage: nanogenmo2021.py [-h] [--table TABLE] [--json JSON]
                        [--synopsis SYNOPSIS] [--story STORY] [--n N]
                        [--create_json] [--create_story] [--create_synopses]

@willf nanogenmo2021

optional arguments:
  -h, --help           show this help message and exit
  --table TABLE        input wiki file
  --json JSON          JSON file pre-synopses
  --synopsis SYNOPSIS  JSON file with Synopsis
  --story STORY        story file
  --n N                number of stories to generate
  --create_json        create json file
  --create_story       create story file
  --create_synopses    create synopsis file
```

That is, something like:

```bash
python nanogenmo2021.py --create_json
python nanogenmo2021.py --create_synopses
python nanogenmo2021.py --create_story
```

The prompt, for an original line like this:

```wikipedia
[[The Adventurer (1920 film)|The Adventurer]] || [[J. Gordon Edwards]] || [[William Farnum]], [[Estelle Taylor]] || Historical || [[Fox Film]]
```
is:

> The Adventurer is a historical movie directed by J. Gordon Edwards. It stars William Farnum and Estelle Taylor. Give a synopsis of the movie."
