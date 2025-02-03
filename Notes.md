```csharp
public partial class ChatMessage
{    
    internal ChatMessageRole Role { get; set; }

    internal ChatMessage(ChatMessageRole role)
    {
        Role = role;
    }

    public ChatMessageContent Content { get; } = new ChatMessageContent();
}

```

```csharp
public enum ChatMessageRole
{
    System,
    User,
    Assistant,
    Tool,
    Function,
}
```

```csharp

```

```csharp
public partial class UserChatMessage :ChatMessage
{
    public string ParticipantName { get; set; }
}
```

```csharp
public partial class AssistantChatMessage : ChatMessage
{
    public IList<ChatToolCall> ToolCalls { get; } = new ChangeTrackingList<ChatToolCall>();
}
```

```csharp
public partial class SystemChatMessage : ChatMessage
{
    public SystemChatMessage(string content)
        : base(ChatMessageRole.System, content)
    {
        Argument.AssertNotNull(content, nameof(content));
    }
}
```