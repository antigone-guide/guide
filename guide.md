Lists

Searching in lists:

Adamanthaea was the Cretan nurse of Zeus who suspended his cradle from a tree that he might be found neither on the earth, in the sea, or in heaven, to avoid being murdered by Cronos.

If Cronos or his henchmen were searching for Zeus on earth, sea or in heaven, here's what would happen:

    places = dict(earth=[], sea=[], heaven[], suspended=['Zeus'])
    for location in ('earth', 'sea', 'heaven'):
        if 'Zeus' in location:
            print(f'Zeus found in {location}')

You can try moving Zeus to earth and see that he will be surely found and likely assasinated, which would change the history of the entire world!

Ancients believed that we descend through the cycle of Ages that become progressively more horrible. In the Golden age, there was no strife or conflict, happiness was universal. In the Silver age, women were created and some amount of strife and minor disagreement was introduced. In the Bronze age, conflicts became so sharp that wars started to break out occasionally, and finally in the Iron age the constant war and bloodshed became pervasive.

And after the Iron age, presumably the cycle would repeat -- we'll repeat it 3 times for illustration:

    ages = ['golden', 'silver', 'bronze', 'iron']
    n = 0
    cycle = 0
    age = ages[n]
    while 1:
        print(f'current age: {age}')
        n+=1
        if n>3:
            n = 0
            cycles+=1
            print()
            if cycle>=3:
                break
        age = ages[n]

Classes

You die, I live

Alcestis was the wife of Admetus. She volunteered to die for her husband on the promise of Apollo that Admetus should never die if someone were found to die in his stead.

    death_record = dict(Alcestis=None, Admetus=None)

    class Alcestis:
        def die(self, to_record=None):
            me = self.__class__.__name__
            if death_record[me] is True:
                print('No death!')
                return
            to_record = to_record or me
            print(f'{who} died')
            death_record[to_record] = True

    class Admetus:
        def die(self, to_record=None):
            me = self.__class__.__name__
            if death_record[me] is True:
                print('No death!')
                return
            to_record = to_record or me
            print(f'{who} died')
            death_record[to_record] = True

    alcestis = Alcestis()
    admetus = Admetus()
    alcestis.die('Admetus')
    admetus.die()

Normally, whoever dies will be recorded in the death record, but the `to_record` argument allows you to falsify the record when you are dying. If your record is falsified, you simply won't die!

Note that the methods have the same logic so that both can be inherited from a parent class to avoid repitition, but I've shown two methods in two classes for clarity.


Conditionals

Lovely options: die or be thrown into the sea

Amycus was a famous boxer who challenged all travelers to fight him. Those who refused were thrown into
the sea, those who accepted were killed in the match.  Finally killed by Polydeuces in a match after he
had refused the Argonauts food and water.

    class Amycus:
        power = 99

        def fight(self, opponent):
            if not opponent.agree():
                print(f'{opponent} thrown into the sea')
                return
            if self.power > opponent.power:
                opponent.die()
            else:
                self.die()

        def die(self):
            print(f'{self} dies')

    class RandomGuy:
        power = 10

        def agree(self):
            return True

        def die(self):
            print(f'{self} dies')

    class Polydeuces:
        power = 200

        def agree(self):
            return True

Note that some of the methods can be inherited from the parent class, but for clarity I duplicated some
methods in each class. Here is a little story of Amycus getting an unpleasant surprice once upon a time:

    amycus = Amycus()
    guy = RandomGuy()
    polydeuces = Polydeuces()

    amycus.fight(guy)
    # RandomGuy dies
    amycus.fight(polydeuces)
    # oops, Amycus dies

Note also that when fighting an opponent with the same power level, Amycus still loses, I suppose because
it is sometimes easier to defend and counterattack. But you could also argue that the attacker should get
a bonus due to the element of surprise. For example, Amymone married Enceladus, son of Aegyptus, and
murdered him on their wedding night, not even waiting for the first honeymoon marital arguments and
disagreements, and without doubt using the element of surprise!

Metamorphosis into a stone

There are many examples of metamorphoses in Mythology, but this is a particularly easy example to model:
Anaxarete was a Greek princess who was loved by Iphis, a man of working class. She mocked his love due to
social difference between them, and in despair Iphis hanged himself on the door of her house. She was
completely unmoved at his death, and Aphrodite turned her to stone.

    class Anaxarete(): pass
    class Stone(): pass
    locations = [Anaxarete(), None, None, None, None]

    locations[0] = Stone()

There are various ways to think of metamorphoses and changes: sometimes it can be a complete change into
an object, other times it may be outward change in appearance while keeping some or all of internal
attributes. For example, when Zeus changed into a swan to make love with Leda, he probably didn't wish to
completely and utterly change into a swan and lose all of his memories and powers, that would be my
guess.

In this case it seems to have been a complete change into a stone (if it ever really happened at all).

The other interesting consideration is how to track when something is alive, exists, and where it is
located. In the real world, if an entity transforms into something else, it means that in the specific
location where it was a moment ago, the new form is present and the old form or entity is not located
anywhere else.

And so the simplest way to model this is to replace the first object with the second in the specific
location where it used to be. However if the first object's existence was tracked in some other
structure, for example in another list, it would have to be also updated at the same time. Also if the
entity has some kind of `die()` behaviour, it would probably have to be run depending on circumstances.


Invincible wrestler

Antaeus was a giant and wrestler of Libya, invincible while he touched the earth (his mother Gaea). But
no one can resist the true GOAT and high IQ fighter Heracles, who strangled him while holding him off the
ground. This immediately should remind us how Zeus was able to hide from his vengeful father: by not
being "on earth".

    earth = ['Antaeus']

    class Antaeus:
        power = 100

        def fight(self, opponent):
            if self.power > opponent.power:
                print(f'{opponent} dies')
            else:
                name = self.__class__.__name__
                if name in earth:
                    print(f'I guess it is a draw?')
                else:
                    print(f'{self} dies')

    class Heracles:
        power = 500

        def lift_opponent(self, opponent):
            earth.remove(opponent)


And so the battle begins:

    antaeus = Antaeus()
    heracles = Heracles()
    antaeus.fight(heracles)
    # a draw!
    heracles.lift_opponent(antaeus)
    antaeus.fight(heracles)
    # Oops, why didn't I chain myself to the ground like Andromeda was chained!! It's too late to
    # complain now

Note how the state of standing directly on the Earth is somewhat arbitrarily signified as being in
`earth` list. This means that someone using a jump rope would be on Earth and not on Earth and back on
Earth and so on many times a second, which seems a little silly. But this is a good example of how some
arbitrary agreed significance of a state is perfectly fine as long as the entire program treats it
consistently. Although, to be fair, even though Heracles was never recorded in myths as using jump rope,
going off his reported agility, success against many different types of opponents, I would venture that
he absolutely used jump rope as part of his training. Perhaps after a few seconds off Earth you can be
officially considered as "off Earth"?


