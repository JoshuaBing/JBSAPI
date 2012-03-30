Josh Bing's Steam API

Purpose: Provides users a relatively simple way to parse games from the Steam Community
and execute those games. It also provides methods to manage an internal list of steam games or create a specific list of games.

FIRST STEPS FOR ENSURING THE API WILL WORK CORRECTLY.

1. Call SteamAPI.setProfType(). Takes a boolean as a parameter. Detailed below.
2. Call SteamAPI.setID(). Takes a string. detailed below.
3. Call SteamAPI.updateGames(). detailed below

**setProfType and setID must be called each time the program is run, unless you use the saveSettings and loadSettings methods to save and write the settings to a file in which case, loadSettings must be called to ensure the library will run correctly**

METHODS AND VARIABLES

SteamAPI.SteamItem - a struct that can be created that represents a steam game and holds its properties. holds the following properties: gameName, gameID, hoursPlayed, genre.

void setProfType(bool type) - Sets the type of profile to be used. pass in true if the user's
steam profile is steamcommunity.com/id/xxxxxxx, pass false if the user's profile is steamcommunity.com/profiles/xxxxxxxxx

void setID(string id) - Sets the users URL id to be used. The last part of the SteamCommunity URL examples above.

bool updateGames() - gets the list of games from the user's steam profile and stores them in the internal list. Returns false if there is an error. Will update hours played as well, and the first 5 games in the list are the last 5 games played.

bool saveSettings() - Writes the profile type and ID to disk in "settings.ini" Returns false if there is an error

bool loadSettings() - loads the Profile Type and ID from disk into the respective variables. This can be used in place of setProfType and SetID as long as the file exists Returns false if there is an error

List<SteamAPI.SteamItem> returnList() - Returns the internal game list of SteamItems.

SteamAPI.SteamItem returnGame(string ID) - Returns a SteamItem based on the supplied game ID. 

SteamAPI.SteamItem returnGame(int index) - Returns a SteamItem at the supplied index. 

void launchGame(string id) - Launches a game based on the supplied ID. Steam handles all error checking here.

void launchGame(SteamAPI.SteamItem item) - Launches a game based on the supplied Item. Again, Steam Handles the checking.

int numElementsInList() - returns the number of items in the internal list.

void addSteamItem(SteamAPI.steamItem toAdd) - Adds a steam Item to the internal list.

void removeSteamItem(SteamAPI.SteamItem toRemove) - removes a specified steam item from the list.

void overrideList(List<SteamAPI.SteamItem list) - ovverrides the internal list with a specified list

void setGenre(SteamAPI.SteamItem item, string genre) - sets the genre of a specified item

bool writeList() - writes the list of games to disk in list.ini. format of Game name\nGameID\nHoursPlayed\nGenre\n. Returns false if there is an error

bool writeList(List<SteamAPI.SteamItem> list) - saves a specified list to list.ini. same format. Returns false if there is an error

bool loadList() - loads the contents of list.ini into the internal list. Returns false if unsuccessful.

List<SteamAPI.SteamItem> loadListToSpecific() - returns the contents of list.ini as a list of steam Items. Returns null if unsuccessful.

void displayList() - displays the list 10 items at a time.

void goToProfile() - launches the default browser and navigates to the user's steam community profile.

List<SteamAPI.SteamItem> lastPlayed() - returns the last 5 games a user has played.




OTHER NOTES
All methods have error checking in them. Bool methods will return false if there was an error, void methods will print out a error message and return.
Set profileType and ID at the beginning of the program, as most other methods depend on these two properties.
Steam does error handling in regards to games. If a game is mac only, steam will notify the user it can't be played. If a game doesn't exist, Steam will just load the homepage. If the user doesn't own a game, it's store page will load in steam.
  