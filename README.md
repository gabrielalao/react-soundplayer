## Install

```
npm install react-soundplayer --save
```

## Examples

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { PlayButton, Timer } from 'react-soundplayer/components';
import { withSoundCloudAudio } from 'react-soundplayer/addons';

const clientId = 'YOUR CLIENT ID';
const Player = withSoundCloudAudio(props => {
    let { track, currentTime } = props;

    return (
      <div className="custom-player">
        <PlayButton
          className="custom-player-btn"
          onPlayClick={() => {
            console.log('play button clicked!');
          }}
          {...props} />
        <h2 className="custom-player-title">
          {track ? track.title : 'Loading...'}
        </h2>
        <Timer 
          className="custom-player-timer"
          duration={track ? track.duration / 1000 : 0} 
          currentTime={currentTime} 
          {...props} />
      </div>
    );
});

const App = () => {
  return (
    <Player
      clientId={clientId}
      resolveUrl={resolveUrl}
      onReady={() => console.log('track is loaded!')} />
  );
};

ReactDOM.render(
  <App />, 
  document.getElementById('#app')
);
```

### Custom Audio Example

It is also easy to built players **without** using SoundCloud API. You just need to pass audio source via `streamUrl` and all other necessary track meta information can be passed as custom props. Also you can choose `preloadType`, according to https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio#Attributes, by default this property is equal to 'auto'.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { PlayButton, Timer } from 'react-soundplayer/components';

// it's just an alias for `withSoundCloudAudio` but makes code clearer
import { withCustomAudio } from 'react-soundplayer/addons';

// audio source
const streamUrl = 'https://example.org/path/to/file.mp3';

// some track meta information
const trackTitle = 'Great song by random artist';

const AWSSoundPlayer = withCustomAudio(props => {
  const { trackTitle } = props;

  return (
    <div>
      <PlayButton {...props} />
      <h2>{trackTitle}</h2>
      <Timer {...props} />
    </div>
  );
});

class App extends React.Component {
  render() {
    return (
      <AWSSoundPlayer
        streamUrl={streamUrl}
        trackTitle={trackTitle} 
        preloadType="auto" />
    );
  }
}

ReactDOM.render(<App />, document.getElementById('app'));
```**MIT Licensed**
