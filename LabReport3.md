# Lab Report 3
By: Emmett Pangan

## The `grep` command

### The `-r` flag
Source: [GNU grep 3.8 Manual](https://www.gnu.org/software/grep/manual/grep.html#Command_002dline-Options)

The `-r` flag is used to grep through the given directory recursively, allowing it to look at files in subdirectories as well. This is useful because it allows one to avoid using an extra `find` command when attempting to search through all files contained by a directory.

The below example shows the use of the `-r` flag to find every instance of the pattern `"Canaveral"` for all text files contained in the `written_2` directory. Every matching line is printed.
```
$ grep -r "Canaveral" written_2/
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:Port Canaveral and Orlando
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:Many cruises to the Bahamas depart from Port Canaveral on Florida’s east coast, about halfway up the peninsula. This is an ideal jumping off point for a number of attractions of worldwide fame — the pleasures of Orlando and Walt Disney World and other theme parks are only 50 minutes away. Even closer, just 20 minutes away from the cruise port, is Cape Canaveral and the Kennedy Space Center.
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:On Cape Canaveral stands one of the most advanced complexes of technological gadgetry anywhere — the John F. Kennedy Space Center. Spread over 220 sq miles (570 sq km), the vast base is an engineer’s dream-come-true. The visitors center has a comprehensive collection of lunar modules, rockets, and space shuttle and skylab hardware; at the IMAX cinema, which runs almost continuously throughout the day, you can watch fantastic documentaries of launches, flights, and space walks.
written_2/travel_guides/berlitz2/Bahamas-WhereToGo.txt:Disney Cruises run from Port Canaveral, stop at Nassau for a day, and then move on to Disney’s private Bahamian hideaway, “Castaway Cay,” for days of fun and relaxation. Cruises can be combined in packages that include time at Walt Disney World theme park and a Disney hotel within the park.
```

The below example shows the use of the `-r` flag to find every instance of the pattern `"vacillation"` for all text files contained in the `written_2` directory. Every matching line is printed.
```
$ grep -r "vacillation" written_2/
written_2/non-fiction/OUP/Berk/ch2.txt:Anselmo’s resulting disorganized behavior and dependency prompt additional parental vacillation—sometimes refusals to help, at other times maladaptive helping—along with exasperation and criticism. Talia and Jim can be heard saying impatiently, “You aren’t any good at this!” “Can’t you do anything?”11 Soon a barrier forms between Anselmo and the task he had previously wanted to master, and his motivation wanes.
written_2/travel_guides/berlitz1/HistoryFrance.txt:        advisors and the king’s own weakness and vacillation led to the
```
### The `-n` flag
Source: [GNU grep 3.8 Manual](https://www.gnu.org/software/grep/manual/grep.html#Command_002dline-Options)

The `-n` flag is used to print the line number for lines that match the given pattern in addition to printing the line itself. This is useful because it allows one to determine the exact location of every matching pattern in a file.

The below example shows the use of the `-n` flag to find the line numbers of lines that contain the pattern `"Vermeer"` in the various Amsterdam travel guide text files.
```
$ grep -n "Vermeer" written_2/travel_guides/berlitz2/Amsterdam-*.txt
written_2/travel_guides/berlitz2/Amsterdam-History.txt:32:Rich merchants needed banks and a support infrastructure, which developed quickly in the city. People flooded in to take advantage of the new commercial opportunities, the population rose rapidly and the old medieval city simply could not cope. It was still very much within the boundaries set almost 150 years before. Plans were made for a series of new canals forming in a ring or girdle around the old medieval horseshoe — three in all, Herengracht, Keizersgracht, and Prinsengracht. The canal side lots were sold to the wealthy of the city who built the finest houses they could afford. The confidence of the city brought opportunities for the arts and the burgeoning sciences. The artists Rembrandt, Frans Hals, Vermeer, and Paulus Potter were all working in this era, their work much in demand by the merchant classes. At the same time the Guild of Surgeons was learning about the physiology of the body at their meeting place in the Waag, helped by Antonie van Leeuwenhoek who had invented the microscope.
written_2/travel_guides/berlitz2/Amsterdam-WhereToGo.txt:74:Johannes Vermeer (1632–1675) is also well-represented, and his effective use of light can be clearly seen in The Kitchen Maid, painted in 1660, which is one of the gallery’s best-loved pieces. There are paintings by Frans Hals, the founding artist of The Dutch School, along with a collection of Dutch artists influenced or schooled by the masters. Rembrandt was a prolific teacher and his pupils produced work so similar to his that in later years many were initially mistaken for the great artist’s work.
```

The below example shows the use of the `-n` flag to find the line numbers of lines that contain the pattern `"Chrysler"` for all text files contained in the `written_2` directory.
```
$ files=`find written_2/ -name "*.txt"`
$ grep -n "Chrysler" $files
written_2/non-fiction/OUP/Rybczynski/ch2.txt:17:Bryant Park also offers distant views of two of Manhattan’s most distinctive skyscrapers: the Chrysler Building and the Empire State Building. The Chrysler Building started life as a speculative office building. In 1927, the architect William Van Alen, influenced by the recent Parisian exhibition of the arts décoratifs, designed a skyscraper in a style that has come to be known as Art Deco. When the plans were finished, but before construction had begun, the design and the building site were bought by the automobile magnate Walter P. Chrysler. Chrysler wanted the building to serve as a billboard for his company. Van Alen obligingly grafted on eagle-head gargoyles (based on hood ornaments), winged radiator caps, a frieze of steel hubcaps, and black brick accents that suggest running boards. The tower’s most distinctive feature was its stainless-steel cap, which held the Cloud Club, a private dining room for Chrysler executives. Today, the flamboyant Chrysler Building is considered a brilliant emblem of the Jazz Age, but it was not an instant success. When it was built it was roundly criticized as frivolous and flashy. “A stunt design,” sniffed The New Yorker. The New York Times likewise derided the blatant commercialism of the architecture.
written_2/non-fiction/OUP/Rybczynski/ch2.txt:18:The Chrysler Building had the distinction of being the world’s tallest building—for a few months, until it was surpassed by the Empire State Building. Although designed at the same time as the Chrysler, the Empire State is quite different in appearance. Its exterior is the architectural equivalent of a gray flannel suit. There is no decoration. The plain limestone walls lack even traditional cornices; chrome-nickel steel mullions extend uninterrupted from the 6th to the 85th floor, accentuating the building’s height. “Ornament is crime” Adolf Loos had proclaimed years before, but the stripped-down appearance of the Empire State Building owed more to an accelerated building schedule—construction took less than eighteen months—than to architectural ideology. In fact, the architects of the skyscraper considered themselves traditionalists. Richmond H. Shreve worked for Carrère & Hastings on the New York Public Library, where he met William Lamb, a recent Ecole graduate. After Carrère’s unfortunate death in an auto accident and Hastings’ retirement, Shreve and Lamb took over the firm (for several years it was called Carrère & Hastings, Shreve & Lamb) and were eventually joined by Arthur Loomis Harmon, who had worked for McKim, Mead & White on the Metropolitan Museum of Art. Despite—or rather because of—their solid Classical roots, Shreve, Lamb and Harmon designed a beautifully proportioned building that became the most famous skyscraper in the world. 
written_2/non-fiction/OUP/Rybczynski/ch2.txt:19:The Empire State Building has one whimsical touch. The final plans called for the skyscraper to end with a flat roof over the 85th floor—1,050 feet, precisely calculated to be two feet higher than the top of the Chrysler Building’s spire. Then, before construction began, the owners decided that two feet was not enough, and ordered the architects to add a 200-foot tower to the top of the building.* This was to be not merely a decorative spire but a functioning symbol of the modern age, a mooring tower for airships. Instead of dropping transatlantic travelers off at Lakehurst, N.J., the thousand-foot-long dirigibles would fly right into Manhattan and hook themselves up to the top of the Empire State Building. Passengers would disembark to an observation platform and descend by elevator to a lounge and customs area on the 86th floor. Most experts, including Hugo Eckener, commander of the Graf Zeppelin, doubted that it could be done. It was hard enough to dock the unwieldy leviathans at ground level, never mind 1,250 feet up in the air. The experts proved to be right, and no airship passengers ever landed atop the Empire State.1 Yet the rocket-shaped tower, with its cast aluminum buttresses and gleaming conical top, is the perfect fanciful crown for this rather solemn skyscraper.
written_2/non-fiction/OUP/Rybczynski/ch2.txt:23:Bryant Park chronicles a hundred years of changing architectural fashions. Buildings are sometimes referred to as timeless, as if this were the highest praise one could bestow. That is nonsense. The best buildings, like the Chrysler or the New York Public Library or the RCA, are precisely of their time. That is part of the pleasure of looking at buildings from the past. They reflect old values and bygone virtues and vices: the self-confidence of the library, the cheerful boosterism of Chrysler, the sobriety of RCA. Even the bland goofiness of the Grace Building recalls the naïve optimism of an earlier era. That is why old buildings are precious, that is why we fight to preserve them. It is not only because we think them beautiful, or significant. It is also because they remind us of who we once were. And of who we might be again, for old buildings also inspire. The ruins of ancient Rome inspired the Renaissance architects. The palazzos of Renaissance Italy inspired Charles McKim. And the memory of McKim’s Pennsylvania Station inspired David Childs of Skidmore, Owings & Merrill to transform McKim’s old Post Office Building into a projected railroad terminal for the city.
written_2/travel_guides/berlitz2/Berlin-WhereToGo.txt:47:Reduced by war and the Wall to a bleak no-man’s-land, the square that was at one time the busiest in Europe has burst back into life in the most invigorating fashion. What was once a scar on the landscape, epitomizing the division of the city and country, is now a thriving arts, entertainment, shopping and business center. The impact of the towering, modern buildings, made almost predominantly from glass, is breathtaking. Investment from corporations such as Daimler-Chrysler and Sony has resulted in the construction of shopping malls, a theater, casino, a splendid hotel, cinemas, and a film museum.
```
### The `-i` flag
Source: [GNU grep 3.8 Manual](https://www.gnu.org/software/grep/manual/grep.html#Command_002dline-Options)

The `-i` flag is used to ignore the case of the given pattern when attempting to find matching lines. When matching letters, this means that the lowercase and uppercase forms of each letter are treated as the same. This is useful because it generalizes a pattern, allowing it to match every case.

The below example shows the use of the `-i` flag to find all instances of the pattern `"wow"` (not case-sensitive) for all text files contained in the `written_2` directory.
```
$ files=`find written_2/ -name "*.txt"`
$ grep -i "wow" $files
written_2/non-fiction/OUP/Berk/ch1.txt:Ben: Wow! Let’s look for Paua shells!
written_2/travel_guides/berlitz1/WhatToLasVegas.txt:        On the other end of the scale, the Tower/WOW! Multimedia
written_2/travel_guides/berlitz1/WhatToLasVegas.txt:        Records and the Good Guys Electronics, WOW! overwhelms in every way. To 
```

The below example shows the use of the `-i` flag to find all instances of the pattern `"iNsAniTy"` (not case-sensitive) for all text files contained in the `written_2` directory.
```
$ files=`find written_2/ -name "*.txt"`
$ grep -i "iNsAniTy" $files
written_2/non-fiction/OUP/Castro/chB.txt:You keep me away from INSANITY’S hungry jaws;
written_2/travel_guides/berlitz1/WhatToJapan.txt:        grief-stricken insanity. The more somber themes alternate with kyogen      
written_2/travel_guides/berlitz2/Vallarta-WhatToDo.txt:If cliff-diving is a sport and not a form of insanity, Acapulco’s La Quebrada cliff-divers have to be the champs. The sight is not to be believed — except that you absolutely must believe in the authenticity of their kneeling before a shrine to the Virgin of Guadalupe just before plunging head first into a narrow slit of water, 130 feet below. Performances are daily at 1pm, and each evening at 7:15, 8:15, 9:15, and 10:15pm, for roughly $1 US admission to the public viewing platform.
```

### The `-C` flag
Source: [GNU grep 3.8 Manual](https://www.gnu.org/software/grep/manual/grep.html#Command_002dline-Options)

The `-C` flag is used to print the lines surrounding matching lines in addition to printing the matching line itself. The number of lines to print before and after the matching line is specified by a number to be given immediately after the `-C` flag. This is useful because it provides context for a matching line, allowing one to see how it is situated in the larger text.

The below example shows the use of the `-C` flag to print the 2 lines before and after any line matching the pattern `"Utopia"` in `WhatToLasVegas.txt`.
```
$ grep -C 2 "Utopia" written_2/travel_guides/berlitz1/WhatToLasVegas.txt
        newsweeklies, CityLife or Las Vegas Weekly.
        Nightclubbing has come of age in Las Vegas, thanks to a   
        resurgence of dance music and the city’s population boom. Club Utopia
        (Tel. 702/390-4650), on the Strip but not in a hotel, may be
        single-handedly responsible for reviving the dying Las Vegas nightclub
```

The below example shows the use of the `-C` flag to print the 1 line before and after any line matching the pattern `"Celtics"` for all text files contained in the `written_2` directory.
```
$ files=`find written_2/ -name "*.txt"`
$ grep -C 1 "Celtics" $files
written_2/travel_guides/berlitz2/Boston-WhereToGo.txt-The last Freedom Trail stop in the North End is Copp’s Hill Burying Ground, which has a fine view across the river to Charlestown. Sexton Robert Newman, preacher Cotton Mather, and Prince Hall, a free black who founded the Negro Freemasons, are all buried here. Note too the pockmarks on some of the headstones caused by the British who used them for target practice before the Battle of Bunker Hill (see page 16).
written_2/travel_guides/berlitz2/Boston-WhereToGo.txt:Head west down Commercial and Causeway streets, and you will soon reach North Station and the site of the old Boston Garden, the beloved arena for the Bruins ice hockey and the Celtics basketball teams until 1995. FleetCenter (Tel. 624-1000 for information on events) has now replaced it.
written_2/travel_guides/berlitz2/Boston-WhereToGo.txt-Charlestown 
--
written_2/travel_guides/berlitz2/Boston-WhereToGo.txt-There are also laser and stargazing shows in the Planetarium, and brilliant 3-D films shown in the Mugar Omni Theater. River trips offering good views of Back Bay leave from the Galleria and the Science Museum (see page 110).
written_2/travel_guides/berlitz2/Boston-WhereToGo.txt:Nearby, on the downtown side of the river, the new temple of this sport- crazy town rises beside North Station. In 1995 FleetCenter replaced the old Boston Garden where fans had cheered on such legends as Bobby Orr of the Boston Bruins and Larry Bird of the Celtics. Tours are given of the new facility.
written_2/travel_guides/berlitz2/Boston-WhereToGo.txt-Day Trips from Boston
```
