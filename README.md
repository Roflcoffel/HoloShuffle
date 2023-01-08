# HoloShuffle
a webapp for finding hololive songs, sung by other members.  
他のホロメンが歌ってくれたホロライブソングを探すためのウェブアプです

## Github Issues
if you know of more songs, and want to help.  
I would really appreciate it if you could create an issue here on github.

and also format it like this.

    "Suisei": [                                    // Singer name
        {
            "youtube_id": ["3zd5C_6jMQ4&t=1690s"], // last part of the youtube url.
            "title": "I'm Your Treasure Box",      // title of the song.
            "by": "Marine"                         // person who made the song.
        },
    ]

if the song is by a small group (2-5) use "by": "small_group"  
if the song is by a big group (5+) use "by": "big_group"

would also be helpful if the title of the issue included the youtube_id.

and of course if you know how to create a pull request then do that instead.

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
