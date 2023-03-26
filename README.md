# @aberoth-community/overheard
A simple Aberoth ["Overheard"](https://aberoth.com/highscore/overheard.html) scraper library & cli.

### Usage:
```javascript
import { OVERHEARD_SCHOOL_NAMES, Overheard } from '@aberoth-community/overheard'

// === Creating a new instance ===
const over = new Overheard(
  // Scraper options
  {
    time: 10e3,
    headers: {}
  },
  // Scraper cache
  {
    online: 50,
    moon: 'full',
    scrolls: {
      [OVERHEARD_SCHOOL_NAMES.RED]: 'dark',
    }
  }
)

// === Listening for events ===
over
  .on('online', console.log)  // 100
  .on('moon', console.log)    // nearly_full
  .on('scrolls', console.log) // { name: 'necromancy', phase: 'normal' }
  // About to exit...
  .on('done', () => {
    // ...
  })
  // Start the scraper
  .start()
  // Stop the scraper
  .stop()

// ========= Getters =========
console.log(
  over.scrolls(),  // [{ name, phase }, { name, phase }, ...]
  over.moon(),     // nearly_full
  over.online(),   // 100
)
```

### Command-line usage:
> `./overheard --help`
```
Usage: overheard [options]

Options:
  -t, --time <time>  scan interval
  -q, --quiet        disable output (default: false)
  -v, --version      output the version number
  -h, --help         display help for command
```

### Shell scripting:
> See: [scripts/sqlite.sh](scripts/sqlite.sh), [scripts/popen.py](scripts/popen.py)
```bash
./overheard -i 10s \
  | xargs -I {} bash -c 'command {}'
```
