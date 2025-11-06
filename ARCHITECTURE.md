# 📊 APP ARCHITECTURE DIAGRAM

## Component Hierarchy

```
ChatUICloneApp (main.dart)
│
└─── MaterialApp
     │
     ├─── Theme: AppTheme.lightTheme()
     │
     └─── Home: ChatScreen (StatefulWidget)
          │
          ├─── AppBar
          │    ├─── Avatar (CircleAvatar + Online Indicator)
          │    ├─── Bot Name & Status
          │    └─── Action Buttons (video, call, info)
          │
          ├─── Body (Column)
          │    │
          │    ├─── Messages List (Expanded + ListView.builder)
          │    │    │
          │    │    ├─── MessageBubble #1
          │    │    │    ├─── Avatar (if bot)
          │    │    │    ├─── Container (bubble)
          │    │    │    │    └─── Text (message.text)
          │    │    │    ├─── Timestamp
          │    │    │    └─── Avatar (if user)
          │    │    │
          │    │    ├─── MessageBubble #2
          │    │    ├─── MessageBubble #3
          │    │    ├─── ...
          │    │    │
          │    │    └─── TypingIndicator (if bot is typing)
          │    │         └─── Animated dots
          │    │
          │    └─── MessageInput (Custom Widget)
          │         ├─── Emoji Button
          │         ├─── TextField (message input)
          │         ├─── Attachment Button
          │         └─── Send Button (CircleAvatar)
          │
          └─── State Management
               ├─── _messages (List<Message>)
               ├─── _scrollController (ScrollController)
               └─── _isBotTyping (bool)
```

## Data Flow

```
User Types Message
       ↓
MessageInput.onSendMessage()
       ↓
ChatScreen._handleSendMessage()
       ↓
Add to _messages List
       ↓
setState() → UI Updates
       ↓
Auto-scroll to bottom
       ↓
Trigger _generateBotReply()
       ↓
Set _isBotTyping = true
       ↓
Show typing indicator
       ↓
Future.delayed(1 second)
       ↓
Generate bot response
       ↓
Add bot message to _messages
       ↓
Set _isBotTyping = false
       ↓
setState() → UI Updates
       ↓
Auto-scroll to bottom
```

## File Dependencies

```
main.dart
  ├── imports: screens/chat_screen.dart
  └── imports: theme/app_theme.dart

chat_screen.dart
  ├── imports: models/message_model.dart
  ├── imports: widgets/message_bubble.dart
  ├── imports: widgets/message_input.dart
  └── imports: theme/app_theme.dart

message_bubble.dart
  ├── imports: models/message_model.dart
  ├── imports: theme/app_theme.dart
  └── imports: package:intl/intl.dart

message_input.dart
  └── imports: theme/app_theme.dart

app_theme.dart
  └── imports: package:google_fonts/google_fonts.dart

message_model.dart
  └── (no external dependencies)
```

## State Management Flow

```
                    ChatScreen State
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   _messages          _scrollController   _isBotTyping
   List<Message>      ScrollController       bool
        │                  │                  │
        ├─ add()          ├─ animateTo()     ├─ true/false
        ├─ length         └─ maxScrollExtent └─ triggers
        └─ [index]                               indicator
        │
        └─── Triggers setState()
                  │
                  └─── Rebuilds Widget Tree
```

## Message Model Structure

```
Message Class
├── Properties
│   ├── sender: String       ("You" or "AI Bot")
│   ├── text: String         (message content)
│   ├── timestamp: DateTime  (when sent)
│   └── isUser: bool         (true/false)
│
└── Methods
    ├── toJson()    → Map<String, dynamic>
    └── fromJson()  → Message
```

## Theme Structure

```
AppTheme Class
│
├── Colors
│   ├── primaryColor: #0084FF
│   ├── userBubbleColor: #0084FF
│   ├── friendBubbleColor: #E4E6EB
│   ├── backgroundColor: #F0F2F5
│   ├── inputBackgroundColor: #FFFFFF
│   └── onlineIndicatorColor: #31A24C
│
├── Themes
│   ├── lightTheme() → ThemeData
│   └── darkTheme() → ThemeData
│
└── TextStyles
    ├── messageTextUser
    ├── messageTextFriend
    ├── timestampText
    └── senderNameText
```

## Widget Lifecycle

```
ChatScreen Created
       ↓
initState()
  ├── Add welcome message
  └── Initialize ScrollController
       ↓
build() → Renders UI
       ↓
User Interaction
       ↓
setState() → Triggers rebuild
       ↓
build() → Re-renders UI
       ↓
dispose()
  └── Dispose ScrollController
```

## UI Layers (Z-Index)

```
┌─────────────────────────────────┐
│  AppBar (elevation: 2)          │ ← Top Layer
├─────────────────────────────────┤
│  Scaffold Background            │
│  ┌───────────────────────────┐  │
│  │  ListView (Messages)      │  │
│  │  ┌─────────────────────┐  │  │
│  │  │  MessageBubble      │  │  │ ← Message Layer
│  │  │  (with shadow)      │  │  │
│  │  └─────────────────────┘  │  │
│  └───────────────────────────┘  │
├─────────────────────────────────┤
│  MessageInput (elevation: 2)    │ ← Bottom Layer
└─────────────────────────────────┘
```

## Responsive Behavior

```
Keyboard Opens
       ↓
SafeArea adjusts
       ↓
MessageInput moves up
       ↓
ListView shrinks height
       ↓
Messages remain visible
       ↓
User sends message
       ↓
FocusScope.unfocus()
       ↓
Keyboard closes
       ↓
UI returns to normal
```

---

This diagram shows how all components work together to create 
the complete Chat UI Clone application.
