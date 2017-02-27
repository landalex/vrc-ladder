CMPT 373 Project Team Beta
================
Team Members:
        Alex Land,
        Constantin Koval,
        David Li,
        Gordon Shieh,
        Jasdeep Jassal,
        NoorUllah Randhawa,
        Raymond Huang,
        Samuel Kim,

PROJECT INTRO:

    This project is intended to be used by Vancouver Racquet Club to replace the present manual system.
    The program contains the following features:

        - LADDER:
                A ladder is a list of pair/teams that consists of two players each. They are ranked through their
                performances i.e. weekly matches, with the top of the ladder representing the highest ranked players.
                Every week, a pair can choose to play or not play in the upcoming round of matches. The players that
                choose to play are placed in groups of 3 or 4 in which they play with other pairs from the ladder. The
                players that choose to not play are penalised accordingly and so every week, after a round of matches,
                ladder is updated to show the new rankings.
                Some features included in the ladder are:
                    - Adding a pair to the ladder
                    - Removing a pair from the ladder
                    - Editing/Updating a pair


        - MATCHES:
                Every week, matches are automatically generated once the pairs from the ladder confirm their availability
                for that week. A match is a group of 3 or 4 pairs (depending on the total number of active players).
                They are generated in sequential order from top of the ladder to the end so the highest ranked pairs
                play with other pairs close to their ranking to avoid mismatch. The pairs that show up late or miss the
                match are penalised accordingly. The pairs are ranked from their performances in a match and then that
                ranking is used to update the ladder afterwards.
                Some features included in the matches are:
                    - Inputting results for a match
                    - Removing a player from a match
                    - Apply penalties to a player

    Each player would have their own accounts where they can login and see the ladder and upcoming matches for the
    week. This would need them to enter their email and password at the time of registration and then that can be
    used for logging in. Users would be able to change their playing status to specify if they would be playing
    for the upcoming week.



Directory Structure:

    There are three main directories in the project structure:
        - src:
            This is our source root and contains logic for the program. The 'core' directory, as the name suggests,
            contains a list of core classes that represent data on which the project is build upon such as Ladder,
            Pair, Game etc. The logic directory includes the classes that interact with core classes to perform some
            functionalities. ui folder contains classes that are used to start the app and the AppController which
            entertains every API request.

        - test:
            These include JUnit tests written for the above mentioned classes.

        - web:
            Includes html, css, js etc. that are being used to design the front end.


Project Architecture:

    As mentioned above, the classes are divided into their appropriate folders. Main.java or JarEntry.java can be used
    start the application. We run Main.java to run local instances of the app while JarEntry.java is used to restart
    the app after a new deployment. To start the app, we create instances of three classes which run the show, these
    are explained below.

        AppController:
            Every API call/request goes through this class. For all the api routes inside the AppController, there is a
            front end api method as well in api.js. For anything that requires back-end assistance, the api route in
            AppController is called which checks the validity of the request and decides how to handle it. An
            appropriate response is returned upon the completion of the request.

        DBManager:
            This is the hub of the application. To entertain each request, the AppController calls DBManager which
            depending on the type of request knows which class or method to call. DBManager is the only place to
            perform any database transaction and it does this with the help of TransactionManager.

        GameSession:
            The mixed doubles play every Thursday. Each one of these weeks correspond to a game session here. Once, the
            new results are entered in, and ladder is reordered, a new game session is created for the next week.
            A game session holds all the required information such as the ladder itself, the pair's time preferences,
            active pairs, and the reordered ladder after the results are input.

    There are various helping classes apart from these. The accounts folder inside src handles all of the account
    information. Whether it is to login, create a new account, manage existing users or resetting password, all of
    that is handled here. The serialization folder inside src includes all classes that are used to serialize output in
    JSON format which is how we talk with the front end. The core app logic can be found inside three classes inside
    src/logic:
        VrcLadderReorderer reorders the ladder at the end of each game week, or when the admin reorders from the web page.
        VrcScorecardGenerator generates groups dynamically based on the playing status of pairs.
        VrcTimeSelection distributes groups into time slots dynamically based on their preferences.

    For the front end, each html page has a .js class to handle logic and api.js is the front end api library, which is
    used to communicate with the back end.

    As a backup strategy, we use csv backups. CSVReader can be used to import or export csv from the web page. This csv
    would include all information that is necessary to restore the app in any unforeseen scenario.



Build & Run Instructions:

    Clone the repo
    cd prj
    ./gradlew run
