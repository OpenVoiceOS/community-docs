# OCP

![](https://github.com/OpenVoiceOS/ovos_assets/blob/master/Logo/ocp.png?raw=true)

[OCP](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin) stands for OpenVoiceOS Common Play, it is a full fledged
media player

## Introduction 

OCP is a [OVOSAbstractApplication](https://github.com/OpenVoiceOS/OVOS-workshop/blob/dev/ovos_workshop/app.py#L47), this
means it is a standalome but native OVOS applicatiom with full voice integration

OCP differs from mycroft-core in several aspects:

- Can run standalone, only needs a bus connection
- OCP provides it's own intents as if it was a skill
- OCP provides it's own GUI as if it was a skill
- mycroft-core CommonPlay skill framework is disabled when OCP loads
- OCP skills have a dedicated MycroftSkill class and decorators in ovos-workshop
- OCP skills act as media providers, they do not (usually) handle playback
- mycroft-core CommonPlay skills have an imperfect compatibility layer and are given lower priority over OCP skills
- OCP handles several kinds of playback, including video
- OCP has a sub-intent parser for matching requested media types
- AudioService becomes a subsystem for OCP
- OCP also has AudioService plugin component introducing a compatibility layer for skills using "old style audioservice
  api"
- OCP integrates with MPRIS, it can be controlled from external apps, eg KdeConnect in your phone
- OCP manages external MPRIS enabled players, you can voice control 3rd party apps without writing a skill for it via
  OCP

## Skills

Skills provide search results, think about them as media providers/catalogs for OCP

### Music

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Youtube Music| ![](https://github.com/JarbasSkills/skill-youtube-music/blob/master/ui/ytmus.png?raw=true) | no | audio player | Youtube music service with official albums, singles, videos, remixes, live performances and more | yes | [github](https://github.com/JarbasSkills/skill-youtube-music) | [Youtube Music](https://music.youtube.com) |
| Bandcamp| ![](https://github.com/JarbasSkills/skill-bandcamp/blob/dev/ui/logo.png?raw=true) | no | audio player |  Music directly from the artists who make it | yes | [github](https://github.com/JarbasSkills/skill-bandcamp) | [Bandcamp](https://bandcamp.com) |
| Soundcloud| ![](https://github.com/JarbasSkills/skill-soundcloud/blob/dev/ui/soundcloud.png?raw=true) | no | audio player |  Discover and play over 265 million music tracks. the world's largest online community of artists, bands, DJs, and audio creators  | yes | [github](https://github.com/JarbasSkills/skill-soundcloud) | [Soundcloud](https://soundcloud.com) |
| SMOD Nation | ![](https://github.com/JarbasSkills/skill-smod/blob/dev/ui/smod_icon.png?raw=true) | yes | audio player |  Full albums from the best up and coming bands in heavy music. Stoner Rock, Heavy Psych, Doom Metal  | yes | [github](https://github.com/JarbasSkills/skill-smod) | [SMOD](https://www.youtube.com/c/StonedMeadowOfDoom1993) , [666MrDoom](https://www.youtube.com/c/666MrDoom)|
| Sovietwave Radio | ![](https://github.com/JarbasSkills/skill-sovietwave/blob/dev/ui/sovietwave_icon.png?raw=true) | yes | audio player | The best of sovietwave, synthwave, chillwave and electronic music   | yes | [github](https://github.com/JarbasSkills/skill-sovietwave) |  [SovietWave Radio](https://newsovietwave.com/) |
| TrveKvlt | ![](https://github.com/JarbasSkills/skill-trve-kvlt/blob/dev/ui/trvekvlt_icon.png?raw=true) | yes | audio player |  Black Metal  | yes | [github](https://github.com/JarbasSkills/skill-trve-kvlt) |  |
| Underrated Albums | ![](https://github.com/JarbasSkills/skill-underrated-albums/blob/master/ui/underratedalbums_icon.jpg?raw=true) | yes | audio player | Music that deserves a wider audience. Not concentrating on any specific genre, music can be good in all forms. Expect anything from slow grinding funeral doom to poppy electronica.  | yes | [github](https://github.com/JarbasSkills/skill-underrated-albums) | [youtube channel](https://www.youtube.com/c/UnderratedAlbums/about) |
| Chiptune Planet | ![](https://github.com/JarbasSkills/skill-chiptune-planet/blob/master/ui/chiptuneplanet_icon.jpg?raw=true) | yes | audio player | Chiptune / 8-bit covers  | yes | [github](https://github.com/JarbasSkills/skill-chiptune-planet) | [youtube channel](https://www.youtube.com/c/8BitSound) |

### News

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| News | ![](https://github.com/JarbasSkills/skill-news/raw/master/res/icon/news.png?raw=true) | yes | audio player | Latest news from selected rss feeds | yes | [github](https://github.com/JarbasSkills/skill-news) | |

### Internet Radio

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| SomaFM | ![](https://github.com/JarbasSkills/skill-somafm/blob/master/ui/somafm.png?raw=true) | yes | audio player | SomaFM's mission is to search for and expose great new music which people may otherwise never encounter. | yes | [github](https://github.com/JarbasSkills/skill-somafm) | [SomaFM](https://somafm.com) |
| Old World Radio | ![](https://github.com/JarbasSkills/skill-old-world-radio/blob/master/ui/old-world-radio.png?raw=true) | yes | audio player | Fallout Radio - Live 24/7 | yes | [github](https://github.com/JarbasSkills/skill-old-world-radio) | [youtube channel](https://www.youtube.com/channel/UCihCtNZnFkG62U4na9JsPJQ) |
| TuneIn | ![](https://github.com/JarbasSkills/skill-tunein/raw/dev/ui/tunein.png?raw=true) | no | audio player | TuneIn brings together live sports, music, news, and podcasts — hear what matters most to you! | yes | [github](https://github.com/JarbasSkills/skill-tunein) | [TuneIn](https://tunein.com) |
| Shoutcast| ![](https://github.com/JarbasSkills/skill-shoutcast/raw/dev/ui/logo.png?raw=true) | yes | audio player | Shoutcast offers you one of the largest directories with more than 50,000 stations | yes | [github](https://github.com/JarbasSkills/skill-shoutcast) | [Shoutcast](https://shoutcast.com/) |
| Radio Browser | ![](https://github.com/JarbasSkills/skill-radio-browser/raw/dev/ui/logo.png?raw=true) | no | audio player | community driven effort (like wikipedia) with the aim of collecting as many internet radio and TV stations as possible | yes | [github](https://github.com/JarbasSkills/skill-radio-browser) | [radio-browser](https://www.radio-browser.info) |

### AudioBooks

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| LibriVox | ![](https://github.com/JarbasSkills/skill-librivox/blob/master/ui/librivox-logo.png?raw=true?raw=true) | yes | audio player |  Free public domain audiobooks. Read by volunteers from around the world | yes | [github](https://github.com/JarbasSkills/skill-librivox) |  [LibriVox](https://librivox.org) |
| HorrorBabble| ![](https://github.com/JarbasSkills/skill-horrorbabble/raw/dev/res/icon/horrorbabble_icon.png?raw=true) | yes | audio player |  Audio Horror, readings of lovecraftian stories from HorrorBabble | yes | [github](https://github.com/JarbasSkills/skill-horrorbabble) |  [HorrorBabble](https://www.horrorbabble.com) |
| Wayne June Lovecraft| ![](https://github.com/JarbasSkills/skill-wayne-june-lovecraft/raw/master/res/icon/icon.png?raw=true) | yes | audio player | Wayne June readings of H. P. Lovecraft stories | yes | [github](https://github.com/JarbasSkills/skill-wayne-june-lovecraft) |    |
| thoughtaudio| ![](https://github.com/JarbasSkills/skill-thoughtaudio/raw/dev/ui/logo.gif?raw=true) | yes | audio player |  audio books for a selection of classic literature and philosophy titles  | yes | [github](https://github.com/JarbasSkills/skill-thoughtaudio) |  [thoughtaudio](http://thoughtaudio.com) |
| Story Nory| ![](https://github.com/JarbasSkills/skill-storynory/raw/dev/ui/logo.png?raw=true) | yes | audio player |  for children and young adults  | yes | [github](https://github.com/JarbasSkills/skill-storynory) |  [storynory](http://storynory.com) |
| Loyal Books| ![](https://github.com/JarbasSkills/skill-loyalbooks/raw/master/ui/logo.png?raw=true) | yes | audio player | 7000+ Free Public Domain Audiobooks | yes | [github](https://github.com/JarbasSkills/skill-loyalbooks) |  [loyalbooks.com](http://www.loyalbooks.com/) |
| Audio Anarchy| ![](https://www.audioanarchy.org/ahead6.gif?raw=true) | yes | audio player | Audio Anarchy is a project for transcribing anarchist books into audio format | yes | [github](https://github.com/JarbasSkills/skill-audio-anarchy) |  [audioanarchy.org](https://www.audioanarchy.org/) |
| Golden Audiobooks| ![](https://github.com/JarbasSkills/skill-golden-audiobooks/raw/master/ui/logo.png?raw=true) | yes | audio player | 1800+ Free Audiobooks | yes | [github](https://github.com/JarbasSkills/skill-golden-audiobooks) |  [goldenaudiobooks.com](https://goldenaudiobooks.com) |
| Stephen King Audiobooks| ![](https://github.com/JarbasSkills/skill-stephen-king-audiobooks/raw/master/ui/logo.png?raw=true) | yes | audio player | | yes | [github](https://github.com/JarbasSkills/skill-stephen-king-audiobooks) |  [stephenkingaudiobooks.com](https://stephenkingaudiobooks.com) |

### Radio Theatre

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Darker Projects| ![](https://github.com/JarbasSkills/skill-darker-projects/raw/master/ui/logo.png?raw=true) | yes | audio player | audio drama company that presents to you original projects such as Autumn, Five Minute Fears, Madness, Night Terrors, Tales from the Museum, and The Falcon Banner. We also have our fan-fiction interpretations of Batman, Dr. Who, He-Man, Outer Limits, Quantum Leap, and Star Trek  | yes | [github](https://github.com/JarbasSkills/skill-darker-projects) |  [DarkerProjects](http://darkerprojects.com) |
| Epic Horror Theatre| ![](https://github.com/JarbasSkills/skill-epic-horror-theatre/raw/dev/res/icon/icon.png?raw=true) | yes | audio player |  Radio drama adaptions of H. P. Lovecraft | yes | [github](https://github.com/JarbasSkills/skill-epic-horror-theatre) |  [ARTC](https://artc.org) |

### Podcasts

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| The H.P. Lovecraft Literary Podcast| ![](https://github.com/JarbasSkills/skill-hppodcraft/raw/master/res/icon/icon.png?raw=true) | yes | audio player |  Each week, hosts Chad Fifer and Chris Lackey discuss a piece of weird fiction. Talented voice actors bring the text to life. | yes | [github](https://github.com/JarbasSkills/skill-hppodcraft) |  [HPPodcraft](https://hppodcraft.com) |

### Motion Comics

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Lovecraft Comics | ![](https://github.com/JarbasSkills/skill-dagon/raw/master/res/icon/dagon.png?raw=true) | yes | video player | Compilation of Comic adaptations of stories by H. P. Lovecraft | yes | [github](https://github.com/JarbasSkills/skill-dagon) |   |

### TV

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| RTP| ![](https://camo.githubusercontent.com/cf7fb53753e63d2273ca9978f701e263deea03dfd4788016ca7212929867a561/68747470733a2f2f63646e2d696d616765732e7274702e70742f636f6d6d6f6e2f696d672f6368616e6e656c732f6c6f676f732f677261792d6e656761746976652f686f72697a6f6e74616c2f7274702e706e673f773d31303026713d3130303b) | yes | web player | RTP Play - Portuguese TV | yes | [github](https://github.com/JarbasSkills/skill-rtp) | [RTP Play](https://www.rtp.pt/play/direto) |

### Documentary

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| RTDocumentaries | ![](https://github.com/JarbasSkills/skill-rt-documentaries/blob/master/ui/rt_icon.jpg?raw=true) | yes | video player|  RT Documentary offers you in-depth documentary films on topics that will leave no one indifferent | yes | [github](https://github.com/JarbasSkills/skill-rt-documentaries) |  [youtube channel](https://www.youtube.com/c/RTDocumentaryChannel/about) |
| Cinemocracy | ![](https://github.com/JarbasSkills/skill-cinemocracy/raw/master/ui/cinemocracy.png?raw=true) | yes | video player | In the early 1940s, the United States government commissioned some of the best filmmakers to create propaganda in support of the war effort | yes | [github](https://github.com/JarbasSkills/skill-cinemocracy) | [internet archive](https://archive.org/details/cinemocracy) |
| Reddit Documentaries | ![](https://github.com/JarbasSkills/skill-documentaries/blob/dev/ui/documentaries_icon.png?raw=true) | yes | video player |  monitor r/Documentaries| yes | [github](https://github.com/JarbasSkills/skill-documentaries) | [reddit](https://www.reddit.com/r/Documentaries)  |
| Documentary Central | ![](https://github.com/JarbasSkills/skill-documentary-central/blob/master/ui/documentarycentral_icon.jpg?raw=true) | yes | video player |  Documentaries | yes | [github](https://github.com/JarbasSkills/skill-documentary-central) | [youtube channel](https://www.youtube.com/c/DocoCentral/about)  |

### Short Films

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Dust | ![](https://github.com/JarbasSkills/skill-dust/raw/master/res/icon/dust_icon.png?raw=true) | yes | video player |  With cutting-edge short films, daring new series and award-winning feature films, DUST is the world’s premiere sci-fi destination | yes | [github](https://github.com/JarbasSkills/skill-dust) |  [Dust](https://www.watchdust.com) |
| Omeleto | ![](https://github.com/JarbasSkills/skill-omeleto/raw/master/ui/icon.png?raw=true) | yes | video player |   the widest-reaching premier short film platform - a place that showcases one award-winning film each day  | yes | [github](https://github.com/JarbasSkills/skill-omeleto) |  [Omeleto](http://omeleto.com/) |
| TheCGBros | ![](https://github.com/JarbasSkills/skill-cgbros/blob/master/ui/cgbros_icon.jpg?raw=true) | yes | video player | We are relentless curators of the most inspirational and insightful examples in Computer Graphics Imagery from around the world | yes | [github](https://github.com/JarbasSkills/skill-cgbros) |  [youtube channel](https://www.youtube.com/c/TheCGBros/about) |

### Cartoons

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Public Domain Cartoons | ![](https://github.com/JarbasSkills/skill-public-domain-cartoons/blob/master/ui/pd-cartoons.png?raw=true) | yes | video player |  public domain cartoons from around youtube | yes | [github](https://github.com/JarbasSkills/skill-public-domain-cartoons) |   |
| r/fullcartoonsonyoutube | ![](https://github.com/JarbasSkills/skill-reddit-cartoons/raw/master/ui/logo.png?raw=true) | yes | video player |  monitor r/fullcartoonsonyoutube for cartoons | yes | [github](https://github.com/JarbasSkills/skill-reddit-cartoons) | [reddit](https://www.reddit.com/r/fullcartoonsonyoutube)  |
| Retro Toons | ![](https://github.com/JarbasSkills/skill-retrotoons/raw/master/ui/retrotoons_icon.jpg?raw=true) | yes | video player |  All of your favorite shows, movies and cartoons from iconic brands like Flinstones, Felix the Cat, Popeye, The Three Stooges, Wacky and Packy, Gumby collection, Superman Original Series and more. | yes | [github](https://github.com/JarbasSkills/skill-retrotoons) | [youtube channel](https://www.youtube.com/c/RetroToonsTV/about)  |
| Film Chest Vintage Cartoons | ![](https://github.com/JarbasSkills/skill-film-chest-vintage-cartoons/raw/master/ui/filmchest.gif?raw=true) | yes | video player |  classic animated cartoons from the 1930's and 1940's! All these cartoons have been transferred from original prints and digitally remastered | yes | [github](https://github.com/JarbasSkills/skill-film-chest-vintage-cartoons) | [FilmChest](http://www.filmchest.com)  |

### Silent Movies

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Silent Hall of Fame| ![](https://github.com/JarbasSkills/skill-silent-hall-of-fame/blob/master/ui/silent_hof_icon.gif?raw=true) | yes | video player | Silent Hall of Fame is the only place where we actively work to bring back from oblivion the names and legacy of formerly illustrious silent movie stars, which have made a major contribution to the industry and the world but do not have a star on the Hollywood Walk of Fame. | yes | [github](https://github.com/JarbasSkills/skill-silent-hall-of-fame) | [internet archive](https://archive.org/details/silenthalloffame) ||

### Black and White Movies

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| PicFixer Feature Films | ![](https://github.com/JarbasSkills/skill-picfixer/blob/master/ui/picfixer.png?raw=true) | yes | video player | COMEDY, DRAMA, ADVENTURE, MYSTERY, ROMANCE, SCI-FI, HORROR, WESTERNS, DOCUMENTARIES, EXPLOITATION. NOSTALGIC DOUBLE-FEATURE THEATER PROGRAMS You will find them all in this free movie loft | yes | [github](https://github.com/JarbasSkills/skill-picfixer) | [internet archive](https://archive.org/details/feature_films_picfixer) |
| Classic Sci Fi Horror Collection | ![](https://github.com/JarbasSkills/skill-classic-scifi-horror/raw/master/ui/scifihorror.png?raw=true) | yes | video player | Science Fiction and Horror films: monsters and aliens, space and time travel, experiments gone wrong, unimagined disasters. | yes | [github](https://github.com/JarbasSkills/skill-classic-scifi-horror) | [internet archive](https://archive.org/details/SciFi_Horror) |
| Comedy Films| ![](https://github.com/JarbasSkills/skill-comedy-films/blob/master/ui/comedyfilms_icon.gif?raw=true) | yes | video player | "All I need to make a comedy is a park, a policeman and a pretty girl." - Charlie Chaplin  | yes | [github](https://github.com/JarbasSkills/skill-comedy-films) | [internet archive](https://archive.org/details/Comedy_Films) |
| FilmNoir| ![](https://github.com/JarbasSkills/skill-film-noir/blob/master/ui/filmnoir_icon.gif?raw=true) | yes | video player | Expressionistic crime dramas of the 40s and 50s: tough cops and private eyes, femme fatales, mean city streets and deserted backroads, bags of loot and dirty double-crossers. | yes | [github](https://github.com/JarbasSkills/skill-film-noir) | [internet archive](https://archive.org/details/Film_Noir) |

### Movies

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Peerflix| ![](https://github.com/JarbasSkills/skill-peerflix/raw/master/ui/magnet.png?raw=true) | no | video player|  Provides Torrent streaming support for other skills | yes | [github](https://github.com/JarbasSkills/skill-peerflix) |  [peerflix](https://github.com/mafintosh/peerflix) |
| Kickass Torrents Proxy | ![](https://github.com/JarbasSkills/skill-kickass-torrents-proxy/blob/master/ui/logo.png?raw=true) | no | skill |  search and stream torrents from kickass torrents | yes | [github](https://github.com/JarbasSkills/skill-kickass-torrents-proxy) |  [katcr.to](https://katcr.to) |
| Sumanjay Torrent Proxy | ![](https://github.com/JarbasSkills/skill-sumanjay-torrent-proxy/blob/master/ui/logo.png?raw=true) | no | skill | search and stream torrents | yes | [github](https://github.com/JarbasSkills/skill-sumanjay-torrent-proxy) |  [sumanjay.cf](https://sumanjay.cf) |
| Abirhasan Torrent Proxy | ![](https://github.com/JarbasSkills/skill-abirhasan-torrent-proxy/blob/master/ui/tpb.svg?raw=true) | no | skill |  search and stream torrents - unofficial api for 1337x and the pirate bay | yes | [github](https://github.com/JarbasSkills/skill-abirhasan-torrent-proxy) |  [api.abirhasan.wtf](https://api.abirhasan.wtf/documentation) |
| RARBG| ![](https://github.com/JarbasSkills/skill-rarbg/blob/master/ui/logo.png?raw=true) | no | skill |  search and stream torrents from RARBG | yes | [github](https://github.com/JarbasSkills/skill-rarbg) |  [rarbgapi](https://pypi.org/project/RarbgAPI) |
| reddit movies | ![](https://github.com/JarbasSkills/skill-reddit-movies/raw/master/ui/logo.png?raw=true) | yes | video player |  monitor  r/fullmoviesonyoutube, r/FullLengthFilms, r/exploitation and r/FullSciFiMovies | yes | [github](https://github.com/JarbasSkills/skill-reddit-movies) | [reddit](https://www.reddit.com/r/FullLengthFilms)  |
| Kings of Horror | ![](https://github.com/JarbasSkills/skill-kings-of-horror/blob/dev/ui/logo.png?raw=true) | yes | video player|  Full-length horror movies since 2015  | yes | [github](https://github.com/JarbasSkills/skill-kings-of-horror) |  [kingsofhorror.com](https://kingsofhorror.com) |
| Cult Cinema Classics| ![](https://github.com/JarbasSkills/skill-ccc/blob/dev/ui/ccc_icon.jpg?raw=true) | yes | video player|  CCC is the first stop for cult film freaks, mad movie misfits, cinema aficionados, and all round tv addicts. Dive deep into all moving images the 20th century | yes | [github](https://github.com/JarbasSkills/skill-ccc) |  [youtube channel](https://www.youtube.com/c/CultCinemaClassics/about) |
| MYT Movies| ![](https://github.com/JarbasSkills/skill-mytmovies/blob/master/ui/mytmovies_icon.jpg?raw=true) | yes | video player|  MYT Movie Network streams movies from Hollywood Blockbusters to Indie award winners and everything in between  | yes | [github](https://github.com/JarbasSkills/skill-mytmovies) |  [youtube channel](https://www.youtube.com/c/SuperheroMovieClip/about) |
|  Deep C Digital | ![](https://github.com/JarbasSkills/skill-deepcdigital/blob/master/ui/deepcdigital_icon.jpg?raw=true) | yes | video player| Deep C Digital is one of the largest and trusted independent movie and TV distributors in the United States, providing outstanding content for today’s digital consumers  | yes | [github](https://github.com/JarbasSkills/skill-deepcdigital) |  [youtube channel](https://www.youtube.com/c/DeepCDigital/about) |
| Film&Clips | ![](https://github.com/JarbasSkills/skill-filmsandclips/blob/master/ui/filmsandclips_icon.jpg?raw=true) | yes | video player|  The Best Free&Legal Youtube Cinema Channel  | yes | [github](https://github.com/JarbasSkills/skill-filmsandclips) |  [youtube channel](https://www.youtube.com/c/FilmandClips/about) |
| Full Free Films | ![](https://github.com/JarbasSkills/skill-fff/blob/master/ui/fff_logo.png?raw=true) | yes | video player|  One stop shop for full length movies on Youtube, new movies added every week   | yes | [github](https://github.com/JarbasSkills/skill-fff) |  [youtube channel](https://www.youtube.com/c/FullLengthMoviesFFF/about) |
| Popcornflix| ![](https://github.com/JarbasSkills/skill-popcornflix/blob/master/ui/popcornflix_icon.jpg?raw=true) | yes | video player|  Popcornflix™ is your destination to stream free full-length movies and television series | yes | [github](https://github.com/JarbasSkills/skill-popcornflix) | [popcornflix.com](https://popcornflix.com) |
| Maverick Movies| ![](https://github.com/JarbasSkills/skill-maverickmovies/blob/master/ui/maverickmovies_icon.jpg?raw=true) | yes | video player|  Maverick Entertainment Group, an independent film distributor specializing in niche genre independent films. | yes | [github](https://github.com/JarbasSkills/skill-maverickmovies) |  [youtube channel](https://www.youtube.com/c/MaverickMovies/about) |
| The Midnight Screening| ![](https://github.com/JarbasSkills/skill-midnightscreening/blob/master/ui/midnightscreening_icon.jpg?raw=true) | yes | video player|  New movies every week so make sure you never miss a Midnight Screening | yes | [github](https://github.com/JarbasSkills/skill-midnightscreening) |  [youtube channel](https://www.youtube.com/c/TheMidnightScreening) |
| Mosfilm| ![](https://github.com/JarbasSkills/skill-mosfilm/blob/master/ui/mosfilm_icon.jpg?raw=true) | yes | video player|  Mosfilm's golden collection presents over 1000 Soviet and Russian films | yes | [github](https://github.com/JarbasSkills/skill-mosfilm) |  [youtube channel](https://www.youtube.com/c/Mosfilm_eng/about) |
| V Movies | ![](https://github.com/JarbasSkills/skill-vmovies/blob/master/ui/vmovies_icon.jpg?raw=true) | yes | video player| Full Movies - part of the V Channels Media Group | yes | [github](https://github.com/JarbasSkills/skill-vmovies) |[youtube channel](https://www.youtube.com/c/FilmTrailerZone/about) |
| V Horror | ![](https://github.com/JarbasSkills/skill-vhorror/blob/master/ui/vhorror_icon.jpg?raw=true) | yes |  video player| Full Horror Movies - part of the V Channels Media Group | yes | [github](https://github.com/JarbasSkills/skill-vhorror) |[youtube channel](https://www.youtube.com/user/LordofTearsMovie/about) |
| V Adrenaline | ![](https://github.com/JarbasSkills/skill-vadrenaline/blob/master/ui/vadrenaline_icon.jpg?raw=true) | yes | video player| Full Action Movies - part of the V Channels Media Group | yes | [github](https://github.com/JarbasSkills/skill-vadrenaline) | [youtube channel](https://www.youtube.com/c/ViewsterTVMovies/about) |
| RetroTV | ![](https://github.com/JarbasSkills/skill-retrotv/blob/master/ui/retrotv_icon.jpg?raw=true) | yes | video player| RETRO TV (Retrospective Television) - TV Hits (And misses!) from the 50's-90's  | yes | [github](https://github.com/JarbasSkills/skill-retrotv) | [youtube channel](https://www.youtube.com/c/RETROTVCHANNEL/about) |
| RavenTV | ![](https://github.com/JarbasSkills/skill-raventv/blob/master/ui/raventv_icon.jpg?raw=true) | yes | video player|  Cheesy Horror and Sci-Fi Movies as well as Classic TV Shows | yes | [github](https://github.com/JarbasSkills/skill-raventv) | [youtube channel](https://www.youtube.com/channel/UCUGjJkUlLN7dct9tGtb_Zvg/about) |
| Star Media | ![](https://github.com/JarbasSkills/skill-starmedia/blob/master/ui/starmedia_icon.jpg?raw=true) | yes | video player| Russian movies and tv series, melodrama, war movies, military tv shows, documentary  with english subtitles | yes | [github](https://github.com/JarbasSkills/skill-starmedia) | [youtube channel](https://www.youtube.com/c/StarMediaEN/about) |
| Movie Central | ![](https://github.com/JarbasSkills/skill-movie-central/blob/master/ui/moviecentral_icon.jpg?raw=true) | yes | video player |  Full free movies on YouTube - owned and operated by VA Media / Valleyarm Digital Ltd.  | yes | [github](https://github.com/JarbasSkills/skill-movie-central) | [youtube channel](https://www.youtube.com/c/MovieCentral/about) |
| Horror Central | ![](https://github.com/JarbasSkills/skill-horror-central/blob/master/ui/horrorcentral_icon.jpg?raw=true) | yes | video player |  Horror Central - your destination for horror movies | yes | [github](https://github.com/JarbasSkills/skill-horror-central) | [youtube channel](https://www.youtube.com/c/HorrorMovieChannel/about) |
| Family Central | ![](https://github.com/JarbasSkills/skill-family-central/blob/master/ui/familycentral_icon.jpg?raw=true) | yes | video player |  Family Central - your destination for full free family movies | yes | [github](https://github.com/JarbasSkills/skill-family-central) | [youtube channel](https://www.youtube.com/channel/UCvRI1Nyvj9pAyHPzX7AviWQ/about) |
| Sci-Fi Central | ![](https://github.com/JarbasSkills/skill-scifi-central/blob/master/ui/scificentral_icon.jpg?raw=true) | yes | video player | Science Fiction Movies and Documentary Content for Ancient Aliens, UFO and Paranormal fans | yes | [github](https://github.com/JarbasSkills/skill-scifi-central) | [youtube channel](https://www.youtube.com/c/SFCentral/about) |
| Western Central | ![](https://github.com/JarbasSkills/skill-western-central/blob/master/ui/westerncentral_icon.jpg?raw=true) | yes | video player | Full length Western movies from the 1930s up to the present day | yes | [github](https://github.com/JarbasSkills/skill-western-central) | [youtube channel](https://www.youtube.com/c/WesternCentralChannel/about) |
| World Movie Central | ![](https://github.com/JarbasSkills/skill-worldmovie-central/blob/master/ui/worldmoviecentral_icon.jpg?raw=true) | yes | video player | Selection of Award Winning independent films in multiple languages from all over the world | yes | [github](https://github.com/JarbasSkills/skill-worldmovie-central) | [youtube channel](https://www.youtube.com/c/WorldMovieCentral/about) |
| Youtube Movies | ![](https://github.com/JarbasSkills/skill-youtube-movies/raw/master/ui/logo.png?raw=true) | no | video player | search youtube for full movies | yes | [github](https://github.com/JarbasSkills/skill-youtube-movies) | [Youtube](https://www.youtube.com)|
| PobreTV | ![](https://www1.pobre.tv/images/logo.png) | yes | web player | Filmes, Séries, Animes Online Grátis  | yes | [github](https://github.com/JarbasSkills/skill-pobretv) | [Pobre TV](https://pobre.tv/)|
| WTvFDigitalGrindhouseDriveIn | ![](https://github.com/JarbasSkills/skill-WTvFDigitalGrindhouseDriveIn/raw/master/ui/logo.jpg?raw=true) | yes | video player| WTvF! Grindhouse and Drive-In: #1 in exploitation movies on youtube | yes | [github](https://github.com/JarbasSkills/skill-WTvFDigitalGrindhouseDriveIn) | [youtube channel](https://www.youtube.com/c/WTvFDigitalGrindhouseDriveIn/about) |

### Video

| skill name | icon | ocp menu | playback type | description | setup.py | source | website |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Simple Youtube| <img src='https://github.com/JarbasSkills/skill-simple-youtube/blob/master/ui/ytube.jpg?raw=true' width='50' height='50' style='vertical-align:bottom'/> | no | video player | Youtube videos | yes | [github](https://github.com/JarbasSkills/skill-simple-youtube) | [Youtube](https://www.youtube.com) |


