# atom-gibberwocky

Gibberwocky Live Coding Plugin for Atom

Gibberwocky is a live-coding environment for Ableton Live using WebSocket and a max/msp patch collection. Gibberwocky is based on Gibber and developed by @charlieroberts

***This is the first working version and will be heavily improved.***

## Installation

- Install [gibberwocky](https://github.com/charlieroberts/gibberwocky)
- Clone or download this plugin and install it by changing into the package directory and running "apm install" and "apm link"
- Restart Atom and add the custom keymap to your keymappings: Atom -> Keymap
- Hit "alt-shift-enter" or click "Packages -> gibberwocky -> Toggle" to start the session

## How to use
- Submit every line of code by selecting it and hitting alt-shift-enter
- It's handy to keep Ableton in sight since there is no visual representation of the lom right now
- Keep in mind the transport needs to be running for sequences to play

## Custom Keymappings

```
'atom-workspace':
  'alt-shift-enter': "gibberwocky:toggle"
```

## Troubleshooting

- Ask for help at: https://talk.lurk.org/channel/gibber
- If you find that you have to manually highlight a line before the alt-shift-enter key map works you can try the following (tested on Windows 10)

Edit the key map like so:

```
'atom-workspace atom-text-editor:not([mini])':
  'alt-shift-enter': "gibberwocky:toggle"
  'ctrl-enter': "custom:gibberwocky-execute"
```

Edit your init.coffee with:

```
atom.commands.add 'atom-text-editor', 'custom:gibberwocky-execute', (evt) ->
  editor = atom.workspace.getActiveTextEditor()
  editor.selectLinesContainingCursors()
  atom.commands.dispatch evt.target, 'gibberwocky:toggle'
  atom.commands.dispatch(evt.target, 'editor:move-to-end-of-line')
```

This will allow you to use ctrl-enter while retaining the alt-shift-enter keymap.  After the command is executed it moves the cursor to the end of the next line
