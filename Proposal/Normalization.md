CineTrace Database Normalization
First Normal Form (1NF)

The database schema satisfies First Normal Form because all tables contain atomic values only, meaning each attribute stores a single value and there are no repeating groups or multivalued fields.

Directors
Each director has a unique director_id.
Attributes such as name, nationality, and birth_year store single values only.
No repeating columns exist.
Cinematographers
Each cinematographer record contains atomic values only.
cinematographer_id uniquely identifies each row.
Films
Each film is uniquely identified by film_id.
Attributes like title, country, language, and runtime_min contain single values.
Genres, crew members, and movements are not stored as comma-separated lists and were separated into junction tables.
Genres
Each genre contains one unique genre name.
No multivalued attributes exist.
Film_Genres
Stores one film–genre relationship per row.
Composite key (film_id, genre_id) ensures uniqueness.
Influence_Links
Each row stores a single influence relationship between two films.
influence_type and evidence_url are atomic attributes.
Cinematic_Movements
Each movement record stores single-valued attributes only.
Film_Movements
Each row represents one relationship between a film and a movement.
Crew_Members
Crew member information is stored once per person.
No repeating attributes exist.
Film_Crew
Each row stores one crew assignment for one film.
Composite primary key prevents duplicate relationships.
Awards
Each row stores one award record for a film.
No multiple awards are stored in a single row.
Users
User information is stored in atomic fields only.
username and email are unique.
Reviews
Each review contains one rating and one review body.
One row represents one review only.
Watchlists
Each watchlist belongs to a single user.
Attributes are atomic and non-repeating.
Watchlist_Items
Each row stores one film added to one watchlist.
Influence_Votes
Each row represents one user vote on one influence link.
Second Normal Form (2NF)

The schema satisfies Second Normal Form because all non-key attributes are fully dependent on the entire primary key. Tables with single-column primary keys automatically satisfy 2NF, while junction tables use composite keys correctly without partial dependency.

Films
Primary key is film_id.
All attributes depend entirely on film_id.
Directors
All director attributes depend fully on director_id.
Cinematographers
All attributes depend fully on cinematographer_id.
Genres
All attributes depend fully on genre_id.
Film_Genres
Composite primary key: (film_id, genre_id)
No additional attributes depend on only one part of the key.
Film_Movements
Composite primary key: (film_id, movement_id)
Attribute role depends on the complete relationship, not partially on one key.
Film_Crew
Composite primary key: (film_id, person_id)
role and leadp depend on both keys together.
Reviews
All review attributes depend entirely on review_id.
Awards
All award details depend on award_id.
Watchlist_Items
Composite key ensures each row depends on both list_id and film_id.
Influence_Links
All attributes depend completely on link_id.
Influence_Votes
Vote details depend fully on vote_id.
Third Normal Form (3NF)

The schema satisfies Third Normal Form because there are no transitive dependencies. Non-key attributes do not depend on other non-key attributes.

Films
Director and cinematographer information were separated into Directors and Cinematographers tables.
This prevents repeated director details across multiple films.
Film attributes depend only on film_id.
Directors
Director details are stored independently.
No non-key attribute depends on another non-key attribute.
Cinematographers
All attributes depend directly on the primary key only.
Genres
Genre descriptions depend only on genre_id.
Film_Genres
Junction table contains only relationship keys.
No transitive dependencies exist.
Influence_Links
Influence relationships are stored separately from Films.
Prevents repeated influence data inside the Films table.
Cinematic_Movements
Movement details are stored independently from films.
No derived or redundant data exists.
Film_Movements
Relationship data is isolated in a junction table.
No transitive dependency exists.
Crew_Members
Crew member details are stored once only.
Prevents repeated crew information across films.
Film_Crew
Relationship attributes depend only on the composite key.
Awards
Award information is separated from Films to avoid redundancy.
Users
User credentials and roles depend only on user_id.
Reviews
Review information is separated from Users and Films.
Prevents repeated review attributes inside other tables.
Watchlists
Watchlist data depends only on list_id.
Watchlist_Items
Stores only the relationship between watchlists and films.
Influence_Votes
Vote information depends only on vote_id.


Duplicate Removal and Redundancy Elimination

The following normalization decisions were made to remove redundancy and duplication from the database schema:

Director information was removed from the Films table and stored separately in the Directors table.
Cinematographer details were separated into the Cinematographers table to prevent repeated data.
Genres were normalized using the Film_Genres junction table instead of storing multiple genres inside Films.
Crew member information was separated into Crew_Members and Film_Crew tables.
Cinematic movement data was separated into Cinematic_Movements and Film_Movements tables.
Influence relationships were isolated in the Influence_Links table instead of storing influence references directly inside Films.
Reviews were stored in a dedicated Reviews table instead of embedding reviews within Films or Users.
Watchlist relationships were normalized through the Watchlist_Items junction table.
User voting on influence links was separated into the Influence_Votes table.



inal Normalization Result

After applying normalization:

All tables satisfy 1NF, 2NF, and 3NF.
Redundant and repeating data has been eliminated.
Many-to-many relationships were resolved using junction tables.
Foreign key constraints maintain referential integrity.
The schema supports efficient querying, scalability, and reduced update anomalies.