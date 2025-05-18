Description:

    This plugin is a fork of the discontinued plugin “[L4D1 & L4D2] Votekick – no black screen (Coop & Versus)” from Dragokas.

    My motivation of the fork is mainly:
    - fix bugs
    - continue support

Features:

    - translucent menu
    - full versus support
    - kick for 1 hour (adjustable) even if the player used a trick to quit from the game before the vote ends.
    - prevents votekick exploit
    - un-kick (from the same menu)
    - vote announcement
    - no black screen
    - flexible configuration of access rights
    - kick reasons (with translation):

        * See the file: data/votekick_reason.txt

    - all actions are logged (who kick, whom kick, who tried to kick, ip/country/nick/SteamId, reason ...)
    - ability to use deny list (by SteamId or nickname) to prevent specific users from starting the vote:

        * See the file: data/votekick_vote_block.txt

    - auto-add to deny list the users from the "newnames.txt" file in Auto-Name-Changer by Exle plugin.
    - ability to exclude a list of users you may not want to connect for a given time period. Excluded users receive the message "STEAM UserID is banned."
	 
        * See the file: data/votekick_ban.txt (if not present, create it by setting cvar sm_votekick_use_banfile set to "1" in cfg-file)
    
    - the voting kick for the team is as short as possible: in Coop and in Versus the counter vote for an active player is cast automatically (similar to official L4D behaviour)


Logfile location:

    - logs/vote_kick.log

Data file:

    - data/votekick_vote_block.txt - list of users you may want to exclude from the right to vote

        * (SteamId and nicknames with simple mask * are allowed).

    - data/votekick_reason.txt - list of kick reasons (optionally, must be supplied with appropriate translation in file: l4d_votekick.phrases.txt).

    Guide to add more kick reasons:

        - Add new line in data/votekick_reason.txt
        - Edit translation file to add new entry similar to "Rusher" in file: translations/l4d_votekick.phrases.txt
    
    - data/votekick_ban.txt - list of users you may not want to connect for a given time period. Optional. Only read/created (if not present) if cvar sm_votekick_use_banfile = 1 (default: 0).

        * Format: SteamId, Start (Unixtime), Minutes, Self note

    - data/votekick_ban_lastwrite.txt - timestamp file. Optional. Only read/created (if not present) if cvar sm_votekick_use_banfile = 1 (default: 0).

Permissions:

    - by default, vote can be started by player with "k" (StartVote) flag (adjustable).
    - by default, vote can be vetoed or force passed by player with "d" (Ban) flag (adjustable).
    - ability to set a minimum time to allow voting to be repeated.
    - ability to set a minimum number of players to hold a vote.
    - admins cannot target root admin.
    - non-admins cannot target admins.
    - users with lower immunity level cannot target users with higher level.
    - everybody able to start vote kick against users from deny list (regardless of sm_votekick_accessflag ConVar settings).
    - (in versus) users can't target users from opposite team

Settings (ConVars):

    - sm_votekick_delay - def.: 60 - Minimum delay (in sec.) allowed between votes
    - sm_votekick_timeout - def.: 10 - How long (in sec.) does the vote last
    - sm_votekick_announcedelay - def.: 2.0 - Delay (in sec.) between announce and vote menu appearing
    - sm_votekick_kicktime - def.: 3600 - How long player will be kicked (in sec.)
    - sm_votekick_minplayers - def.: 1 - Minimum players present in game to allow starting vote for kick
    - sm_votekick_minplayers_versus - def.: 1 - Minimum players present in team to allow starting vote for kick (Versus gamemode)
    - sm_votekick_accessflag - def.: "" (StartVote) - Admin flag required to start the vote (leave empty to allow for everybody)
    - sm_votekick_vetoflag - def.: "d" (Ban) - Admin flag required to veto/votepass the vote
    - sm_votekick_log - def.: 1 - Use logging? (1 - Yes / 0 - No)
    - sm_votekick_show_kick_reason - def: 0 - Allow to select kick reason? (1 - Yes / 0 - No)
    - sm_votekick_show_bots - def.: 0 - Allow to vote kick survivor bots? (1 - Yes / 0 - No)
    - sm_votekick_show_self - def.: 0 - Allow to self-kick (for debug purposes)? (1 - Yes / 0 - No)
    - sm_votekick_show_vote_details - def.: 1 - Allow to show number of yesVotes - noVotes? (1 - Yes / 0 - No)
    - sm_votekick_use_banfile - def.: 0 - Use file based temporary bans? (1 - Yes / 0 - No)
    - sm_votekick_use_banfile_log - def.: 1 - File based temporary bans: log attempts to join the server? (1 - Yes / 0 - No)
    - sm_votekick_versus_inactive_time - def.: 45 - Time (in sec.) after which an inactive player is considered AFK. In a kick vote against him, he can then only vote manually

Commands:

    - sm_vk - Show menu to select player to vote for kick/unkick
    - sm_votekick - same as sm_vk
    - sm_veto - Allow admin to veto current vote
    - sm_votepass - Allow admin to bypass current vote
    - sm_pass - same as sm_votepass

Requirements:

    - GeoIP extension (included in SourceMod).
    - SourceMod v.1.10+

Languages:

    - English
    - Russian

Installation:

    - copy smx file to addons/sourcemod/plugins/
    - copy l4d_votekick.phrases.txt file to addons/sourcemod/translations/
    - copy data/ .txt files to addons/sourcemod/data/
    - banfile:
      to enable, set sm_votekick_use_banfile = 1 in the cfg file. 	  
      * file data/votekick_ban.txt will be created with next map start/change, if it not already exists.
      There You can add a player's STEAM Id to exclude them from connection
      * file data/votekick_ban_lastwrite.txt will be created with next map start/change, if it not already exists.    
      to disable, set sm_votekick_use_banfile = 0 in the cfg file (effective with the next map change).
    
Credits:

    - D1maxa – for the initial plugin
    - Dragokas – much thanks for his outstanding and inspiring work on which this plugin is based
  
References:
    
    - [L4D1 & L4D2] Votekick (Coop & Versus): https://forums.alliedmods.net/showthread.php?t=349341
