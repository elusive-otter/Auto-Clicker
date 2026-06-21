# AutoClicker — Full Guide
*Made by elusive-otter*

---

## Table of Contents

1. [How to Use the AutoClicker](#1-how-to-use-the-autoclicker)
2. [How to Edit the Script](#2-how-to-edit-the-script)
3. [AutoHotkey v2 Basics](#3-autohotkey-v2-basics)
   - [Variables](#variables)
   - [If Statements](#if-statements)
   - [Functions](#functions)
   - [Loops](#loops)
   - [Hotkeys](#hotkeys)
   - [GUI Basics](#gui-basics)
   - [Timers](#timers)
   - [Mouse & Keyboard Commands](#mouse--keyboard-commands)

---

## 1. How to Use the AutoClicker

### Installation

1. Go to https://www.autohotkey.com/ and download **AutoHotkey v2**
2. Run the installer and follow the steps
3. Once installed, double-click `autoclicker.ahk` — it will open automatically

> If it opens as a text file instead, right-click it → Open With → AutoHotkey v2

---

### The GUI Window

When the script runs, a small window appears with the following controls:

```
┌─────────────────────────────┐
│ ⚡ AutoClicker               │
│ AutoHotkey v2 · by elusive-otter │
├─────────────────────────────┤
│ STATUS        STOPPED       │
│                             │
│ INTERVAL (ms)               │
│ [100]  ──────────────────── │
│ ~ 10.0 clicks/sec           │
│                             │
│ MOUSE BUTTON                │
│ [Left]   Right    Middle    │
│                             │
│ CLICK MODE                  │
│ [Single]   Double           │
├─────────────────────────────┤
│ Start [F6]     Quit [F8]    │
│ F6 = toggle    F8 = quit    │
└─────────────────────────────┘
```

**STATUS** — Shows STOPPED or RUNNING

**INTERVAL** — How many milliseconds between each click
- Type a number directly in the box, or drag the slider
- 100ms = 10 clicks/sec
- 50ms = 20 clicks/sec
- 10ms = 100 clicks/sec

**MOUSE BUTTON** — Which button gets clicked
- The active selection shows brackets: `[ Left ]`

**CLICK MODE**
- Single — one click per interval
- Double — two clicks per interval (double-click)

**Start / Stop** — Begins or pauses clicking

**Quit** — Closes the script completely

---

### Hotkeys

You can control the clicker without touching the window:

| Key | Action |
|-----|--------|
| `F6` | Toggle clicking on or off |
| `F8` | Exit the script |

These work **globally** — even when another window is focused.

---

### Tips

- Position your mouse cursor where you want clicks to land **before** pressing Start
- Use a higher interval (e.g. 500ms) for slower, deliberate clicking
- Use a lower interval (e.g. 10–50ms) for fast clicking in games
- The window is always-on-top so you can adjust settings mid-use
- Press F6 to pause, reposition your mouse, then F6 again to resume

---

## 2. How to Edit the Script

### Opening the Script

Right-click `autoclicker.ahk` and choose **Edit Script** — this opens it in Notepad (or your default text editor). You can also open it in any code editor like VS Code.

For the best experience, install the **AutoHotkey extension for VS Code** — it gives you syntax highlighting and autocomplete.

---

### Changing the Default Interval

Find this line near the top:

```ahk
global intervalMs := 100
```

Change `100` to any value in milliseconds. For example, `50` for 20 clicks/sec.

---

### Changing the Default Mouse Button

Find this line:

```ahk
global clickType := "Left"
```

Change `"Left"` to `"Right"` or `"Middle"`.

---

### Changing the Default Click Mode

Find this line:

```ahk
global clickMode := "Single"
```

Change `"Single"` to `"Double"` if you want double-clicking by default.

---

### Changing the Hotkeys

At the very bottom of the script:

```ahk
F6::ToggleClicker()
F8::ExitApp()
```

Replace `F6` or `F8` with any key you want. Examples:

```ahk
F1::ToggleClicker()     ; Use F1 instead
^F6::ToggleClicker()    ; Ctrl + F6
!F6::ToggleClicker()    ; Alt + F6
+F6::ToggleClicker()    ; Shift + F6
```

---

### Changing the Window Title

Find this line:

```ahk
myGui := Gui("+AlwaysOnTop", "AutoClicker")
```

Replace `"AutoClicker"` with any title you want.

---

### Removing Always-On-Top

Find:

```ahk
myGui := Gui("+AlwaysOnTop", "AutoClicker")
```

Change it to:

```ahk
myGui := Gui("", "AutoClicker")
```

---

### Changing the Auto Walk Key

By default, Auto Walk holds the `W` key. To change it to a different key, find this section near the bottom:

```ahk
ToggleWalk(*) {
    global isWalking
    isWalking := !isWalking
    if isWalking {
        walkLabel.Text := "WALKING"
        btnWalk.Text   := "Stop Walk   [F7]"
        Send("{w down}")
    } else {
        walkLabel.Text := "STOPPED"
        btnWalk.Text   := "Start Walk  [F7]"
        Send("{w up}")
    }
}
```

Replace `{w down}` and `{w up}` with any key. Examples:

```ahk
Send("{a down}")   ; Hold A instead
Send("{Space down}") ; Hold Spacebar
Send("{Up down}")  ; Hold Up arrow key
```

---

### Changing the Auto Jump Key

By default, Auto Jump presses and releases the `Space` key. To change it, find:

```ahk
DoJump() {
    Send("{Space down}")
    Sleep(50)
    Send("{Space up}")
}
```

Replace `{Space}` with any key:

```ahk
Send("{z down}")     ; Press Z instead
Send("{Up down}")    ; Press Up arrow
Send("{LShift down}") ; Press Left Shift
```

---

### Changing the Jump Interval Default

Find this line near the top:

```ahk
global jumpMs := 600
```

Change `600` to any value between 100 and 2000 (milliseconds between jumps).

---

### Changing the Auto Jump Hotkey

At the bottom of the script:

```ahk
F8::ToggleJump()
```

Replace `F8` with any key:

```ahk
F3::ToggleJump()     ; Use F3 instead
^space::ToggleJump() ; Ctrl + Space
!j::ToggleJump()     ; Alt + J
```

---

### Changing the Auto Walk Hotkey

At the bottom of the script:

```ahk
F7::ToggleWalk()
```

Replace `F7` with any key you prefer:

```ahk
F2::ToggleWalk()     ; Use F2 instead
^w::ToggleWalk()     ; Ctrl + W
!w::ToggleWalk()     ; Alt + W
```

---

### Adding a Click Limit

To make the clicker stop after a set number of clicks, add a counter. Find the `DoClick()` function:

```ahk
DoClick() {
    global clickType, clickMode
    if (clickMode = "Double") {
        Click(clickType)
        Sleep(30)
        Click(clickType)
    } else {
        Click(clickType)
    }
}
```

Modify it like this:

```ahk
global clickCount := 0
global clickLimit := 100   ; Stop after 100 clicks — change this number

DoClick() {
    global clickType, clickMode, clickCount, clickLimit
    clickCount += 1
    if (clickCount >= clickLimit) {
        ToggleClicker()
        clickCount := 0
        return
    }
    if (clickMode = "Double") {
        Click(clickType)
        Sleep(30)
        Click(clickType)
    } else {
        Click(clickType)
    }
}
```

---

## 3. AutoHotkey v2 Basics

This section teaches you the fundamentals of AHK v2 so you can confidently modify or extend the script.

---

### Variables

Variables store values. In AHK v2, you assign them with `:=`

```ahk
name := "yourname"
speed := 100
isRunning := false
```

To declare a variable accessible everywhere in the script, use `global`:

```ahk
global score := 0
```

To update it inside a function, declare it global again inside the function:

```ahk
global score := 0

AddPoint() {
    global score
    score += 1
}
```

**Types:**
- String: `"hello"`
- Number: `42` or `3.14`
- Boolean: `true` or `false`

---

### If Statements

```ahk
x := 10

if (x > 5) {
    MsgBox("x is greater than 5")
} else if (x = 5) {
    MsgBox("x equals 5")
} else {
    MsgBox("x is less than 5")
}
```

**Comparison operators:**

| Operator | Meaning |
|----------|---------|
| `=` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

**Logical operators:**

```ahk
if (x > 0 && x < 100)   ; AND
if (x = 0 || x = 100)   ; OR
if (!isRunning)           ; NOT
```

**Ternary (shorthand if/else):**

```ahk
label := (isRunning) ? "RUNNING" : "STOPPED"
; If isRunning is true → "RUNNING", otherwise → "STOPPED"
```

---

### Functions

Functions are reusable blocks of code. In AHK v2:

```ahk
; Define a function
SayHello(personName) {
    MsgBox("Hello, " . personName . "!")
}

; Call it
SayHello("ouimiles")
```

Functions can return values:

```ahk
Add(a, b) {
    return a + b
}

result := Add(3, 4)   ; result = 7
```

The `*` in function parameters means "accept any extra arguments" — you'll see this in event handlers:

```ahk
btnStart.OnEvent("Click", StartClicking)

StartClicking(*) {
    ; The * lets AHK pass extra event info without errors
    MsgBox("Started!")
}
```

---

### Loops

**Loop a set number of times:**

```ahk
loop 5 {
    MsgBox("This is loop number " . A_Index)
}
; A_Index is a built-in variable that tracks which iteration you're on
```

**While loop:**

```ahk
count := 0
while (count < 10) {
    count += 1
}
```

**Loop with break:**

```ahk
loop {
    count += 1
    if (count >= 5)
        break   ; Exit the loop
}
```

---

### Hotkeys

Hotkeys map a key press to an action:

```ahk
F1::MsgBox("You pressed F1!")

; Modifiers:
; ^ = Ctrl
; ! = Alt
; + = Shift
; # = Win key

^c::MsgBox("You pressed Ctrl+C")
!F4::ExitApp()           ; Alt+F4 to quit
```

To call a function from a hotkey:

```ahk
F6::ToggleClicker()
```

To disable a hotkey (block the key):

```ahk
F6::return
```

---

### GUI Basics

GUIs let you build windows with buttons, sliders, text, and input fields.

**Creating a window:**

```ahk
myGui := Gui("", "My Window Title")
myGui.Show("w300 h200")   ; Width 300, height 200
```

**Adding elements:**

```ahk
; Text label
myGui.Add("Text", "x10 y10", "Hello World")

; Button
myBtn := myGui.Add("Button", "x10 y40 w100 h30", "Click Me")

; Input box
myEdit := myGui.Add("Edit", "x10 y80 w200 h24", "default text")

; Slider
mySlider := myGui.Add("Slider", "x10 y110 w200 Range1-100", 50)
```

Position options: `x` = horizontal, `y` = vertical, `w` = width, `h` = height

**Handling button clicks:**

```ahk
myBtn.OnEvent("Click", BtnClicked)

BtnClicked(*) {
    MsgBox("Button was clicked!")
}
```

**Reading and setting values:**

```ahk
; Read text from an Edit box
userInput := myEdit.Value

; Set text on a label or button
myLabel.Text := "New text here"

; Set value on a slider or edit
mySlider.Value := 75
```

**Closing event:**

```ahk
myGui.OnEvent("Close", (*) => ExitApp())
```

---

### Timers

Timers run a function repeatedly on an interval:

```ahk
; Start a timer — runs DoSomething() every 500ms
SetTimer(DoSomething, 500)

DoSomething() {
    MsgBox("Tick!")
}

; Stop the timer
SetTimer(DoSomething, 0)
```

This is how the autoclicker works — `SetTimer(DoClick, intervalMs)` fires the click function every `intervalMs` milliseconds.

---

### Mouse & Keyboard Commands

**Mouse clicks:**

```ahk
Click()              ; Left click at current position
Click("Right")       ; Right click
Click("Middle")      ; Middle click
Click(500, 300)      ; Left click at x=500, y=300
Click("Right", 500, 300)  ; Right click at coordinates
```

**Double click:**

```ahk
Click()
Sleep(30)    ; Small delay between clicks
Click()
```

**Move the mouse:**

```ahk
MouseMove(500, 300)        ; Move to x=500, y=300
MouseMove(500, 300, 5)     ; Move slowly (speed 5, default is 2)
```

**Send keyboard input:**

```ahk
Send("Hello World")       ; Type text
Send("{Enter}")           ; Press Enter
Send("{Tab}")             ; Press Tab
Send("^c")                ; Ctrl+C (copy)
Send("^v")                ; Ctrl+V (paste)
Send("{F5}")              ; Press F5
Send("+{Home}")           ; Shift+Home (select to beginning)
```

**Pause execution:**

```ahk
Sleep(1000)    ; Wait 1000ms (1 second)
Sleep(500)     ; Wait half a second
```

**Get mouse position:**

```ahk
MouseGetPos(&mouseX, &mouseY)
MsgBox("Mouse is at " . mouseX . ", " . mouseY)
```

---

### Useful Built-in Variables

| Variable | Value |
|----------|-------|
| `A_Index` | Current loop iteration number |
| `A_TickCount` | Milliseconds since Windows started |
| `A_ScriptDir` | Folder where your script is located |
| `A_ScriptName` | Filename of your script |
| `A_IsCompiled` | True if script is compiled to .exe |

---

### Message Boxes

```ahk
MsgBox("Simple message")

; With title
MsgBox("Message text", "Window Title")

; With buttons — returns which button was pressed
result := MsgBox("Are you sure?", "Confirm", "YesNo")
if (result = "Yes") {
    ; Do the thing
}
```

---

### String Concatenation

Join strings with `.`

```ahk
first := "Hello"
second := "World"
combined := first . " " . second   ; "Hello World"

; Inline with variables
MsgBox("Score: " . score . " points")
```

---

### Comments

```ahk
; This is a single-line comment

/*
   This is a
   multi-line comment
*/
```

---

*That covers everything you need to read, understand, and modify the autoclicker script. Happy scripting!*

*— elusive-otter*
