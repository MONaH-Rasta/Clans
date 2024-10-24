# Clans

About Oxide plugin for Rust. Universal clans with alliance support

Clans plugin for all Oxide supported games.

Better Chat is required to display clan tags in chat! 

## Chat Commands
* `/clan`
* `/clanhelp` - Displays help
* `/clan create <tag>` - Create a new clan
* `/clan join <tag>` - Join a clan if you have a invite

* **Clan Member Commands**
* `/clan leave`- Leave you current clan
* `/c <message>` - Send a message to all clan members

* **Clan Moderator Commands**
* `/clan invite <partialname>` - Invite a player to join your clan
* `/clan invite cancel <partialname/ID>` - Cancel a pending invite
* `/clan kick <partialname/ID>` - Kick a player from your clan

* **Clan Owner Commands**
* `/clan promote <partialname/ID>` - Promote a clan member to clan moderator
* `/clan demote <partialname/ID>` - Demote a clan moderator to clan member
* `/clan disband` - Disband your clan


* **Clan Alliance Commands**
* `/clan ally invite <tag>` - Request an alliance with another clan
* `/clan ally withdraw <tag>` - Revoke an alliance invitation with another clan
* `/clan ally accept <tag>` - Accept an alliance invite
* `/clan ally reject <tag>` - Decline a alliance request
* `/clan ally revoke <tag>` - End a clan alliance
* `/a <message>` - Send a message to all clan members and allied clans

## Configuration
```json
{
  "Clan Options": {
    "Member limit": 8,
    "Moderator limit": 2,
    "Alliance Options": {
      "Enable clan alliances": true,
      "Alliance limit": 2
    },
    "Invite Options": {
      "Maximum allowed member invites at any given time": 8,
      "Member invite expiry time (seconds)": 86400,
      "Maximum allowed alliance invites at any given time": 2,
      "Alliance invite expiry time (seconds)": 86400
    }
  },
  "Role Colors": {
    "Clan owner color (hex)": "#a1ff46",
    "Clan moderator color (hex)": "#74c6ff",
    "Clan member color (hex)": "#fcf5cb",
    "General text color (hex)": "#e0e0e0"
  },
  "Clan Tag Options": {
    "Enable clan tags (requires BetterChat)": true,
    "Tag opening character": "[",
    "Tag closing character": "]",
    "Tag color (hex)": "#aaff55",
    "Allow clan leaders to set custom tag colors (BetterChat only)": false,
    "Tag size": 15,
    "Tag character limits": {
      "Minimum": 2,
      "Maximum": 5
    }
  },
  "Purge Options": {
    "Enable clan purging": true,
    "Purge clans that havent been online for x amount of day": 14,
    "List purged clans in console when purging": true
  },
  "Settings": {
    "Log clan and member changes": false
  },
  "Version": {
    "Major": 0,
    "Minor": 2,
    "Patch": 0
  }
}
```

## API
```csharp
string GetClanOf(string playerID) 
string GetClanOf(ulong playerID) 
string GetClanOf(IPlayer player) 
string GetClanOf(BasePlayer player) // Rust only
string GetClanOf(PlayerSession session) // Hurtworld only
// Returns the clan tag of the specified player
```

```csharp
List<string> GetClanMembers(string playerId) 
// Get clan members for the specified player ID
```

```csharp
bool IsClanMember(string playerId, string otherId) 
// Check if 2 players are clan mates
```

```csharp
bool IsMemberOrAlly(string playerId, string otherId) 
// Check if 2 players are clan mates or clan allies
```

```csharp
bool IsAllyPlayer(string playerId, string otherId) 
// Check if 2 players are in allied clans
```

```csharp
List<string> GetClanAlliances(string playerId) 
// Returns allianced clan tags for the specified player
```

```csharp
JArray GetAllClans() 
// Returns a array of all clan tags
```

```csharp
JObject GetClan(string tag) 
// Returns a JObject containing all of the specified clans information

//Available properties:
// "tag" - (string) clan tag
// "owner" - (string) clan owner id
// "moderators" - (JArray) moderator user id's
// "members" - (JArray) member user id's
// "invited" - (JArray) invited player user id's
// "allies" - (JArray) ally clan tags
// "invitedallies" - (JArray) invited ally clan tags
```

## Hooks
These hooks are for the purpose of updating information within external plugins. They have no return behaviour.

```csharp
OnClanCreate(string tag) 
// Is called when a clan is created
```

```csharp
OnClanUpdate(string tag) 
// Is called when a clan is updated
```

```csharp
OnClanDestroy(string tag) 
// Is called when a clan is disbanded
```

```csharp
OnClanChat(IPlayer player, string message) 
// Called when a player uses clan chat
```

```csharp
OnClanMemberJoined(string userID, List<string> memberUserIDs)
OnClanMemberJoined(string userID, string tag) 
// Called when a player joins a clan
```

```csharp
OnClanMemberGone(string userID, List<string> memberUserIDs)
OnClanMemberGone(string userID, string tag) 
// Called when a player leaves a clan
```

```csharp
OnClanDisbanded(List<string> memberUserIDs) 
OnClanDisbanded(string tag, List<string> memberUserIDs) 
// Called when a clan has been disbanded
```