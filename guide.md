## Lists

### Searching in lists:

Adamanthaea was the Cretan nurse of Zeus who suspended his cradle from a tree that he might be found neither on the earth, in the sea, or in heaven, to avoid being murdered by Cronos.

If Cronos or his henchmen were searching for Zeus on earth, sea or in heaven, here's what would happen:

```python
places = dict(earth=[], sea=[], heaven[], suspended=['Zeus'])
for location in ('earth', 'sea', 'heaven'):
    if 'Zeus' in location:
        print(f'Zeus found in {location}')
```

You can try moving Zeus to earth and see that he will be surely found and likely assasinated, which would change the history of the entire world!

Ancients believed that we descend through the cycle of Ages that become progressively more horrible. In the Golden age, there was no strife or conflict, happiness was universal. In the Silver age, women were created and some amount of strife and minor disagreement was introduced. In the Bronze age, conflicts became so sharp that wars started to break out occasionally, and finally in the Iron age the constant war and bloodshed became pervasive.

And after the Iron age, presumably the cycle would repeat -- we'll repeat it 3 times for illustration:

```python
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
```

## Classes

### You die, I live

Alcestis was the wife of Admetus. She volunteered to die for her husband on the promise of Apollo that Admetus should never die if someone were found to die in his stead.

```python
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
```

Normally, whoever dies will be recorded in the death record, but the `to_record` argument allows you to falsify the record when you are dying. If your record is falsified, you simply won't die!

Note that the methods have the same logic so that both can be inherited from a parent class to avoid repitition, but I've shown two methods in two classes for clarity.


### Conditionals

### Lovely options: die or be thrown into the sea

Amycus was a famous boxer who challenged all travelers to fight him. Those who refused were thrown into
the sea, those who accepted were killed in the match.  Finally killed by Polydeuces in a match after he
had refused the Argonauts food and water.

```python
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
```

Note that some of the methods can be inherited from the parent class, but for clarity I duplicated some
methods in each class. Here is a little story of Amycus getting an unpleasant surprice once upon a time:

```python
amycus = Amycus()
guy = RandomGuy()
polydeuces = Polydeuces()

amycus.fight(guy)
# RandomGuy dies
amycus.fight(polydeuces)
# oops, Amycus dies
```

Note also that when fighting an opponent with the same power level, Amycus still loses, I suppose because
it is sometimes easier to defend and counterattack. But you could also argue that the attacker should get
a bonus due to the element of surprise. For example, Amymone married Enceladus, son of Aegyptus, and
murdered him on their wedding night, not even waiting for the first honeymoon marital arguments and
disagreements, and without doubt using the element of surprise!

### Metamorphosis into a stone

There are many examples of metamorphoses in Mythology, but this is a particularly easy example to model:
Anaxarete was a Greek princess who was loved by Iphis, a man of working class. She mocked his love due to
social difference between them, and in despair Iphis hanged himself on the door of her house. She was
completely unmoved at his death, and Aphrodite turned her to stone.

```python
class Anaxarete(): pass
class Stone(): pass
locations = [Anaxarete(), None, None, None, None]

locations[0] = Stone()
```

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


### Invincible wrestler

Antaeus was a giant and wrestler of Libya, invincible while he touched the earth (his mother Gaea). But
no one can resist the true GOAT and high IQ fighter Heracles, who strangled him while holding him off the
ground. This immediately should remind us how Zeus was able to hide from his vengeful father: by not
being "on earth".

```python
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
```


And so the battle begins:

```python
antaeus = Antaeus()
heracles = Heracles()
antaeus.fight(heracles)
# a draw!
heracles.lift_opponent(antaeus)
antaeus.fight(heracles)
# Oops, why didn't I chain myself to the ground like Andromeda was chained!! It's too late to
# complain now
```

Note how the state of standing directly on the Earth is somewhat arbitrarily signified as being in
`earth` list. This means that someone using a jump rope would be on Earth and not on Earth and back on
Earth and so on many times a second, which seems a little silly. But this is a good example of how some
arbitrary agreed significance of a state is perfectly fine as long as the entire program treats it
consistently. Although, to be fair, even though Heracles was never recorded in myths as using jump rope,
going off his reported agility, success against many different types of opponents, I would venture that
he absolutely used jump rope as part of his training. Perhaps after a few seconds off Earth you can be
officially considered as "off Earth"?

### Dividing the time between Earth and Underworld

Persephone could leave the lower world provided she had eaten no food, however Pluto was informed that
she ate some pomegranate seeds, and she was required to divide her time evenly between the lower world
and the Earth.

```python
import time
earth = 0
underworld = 1
cycle = 0
location = earth

while 1:
    print('location ' + ('earth' if location==earth else 'underworld'))
    print('6 months passed')
    print()
    time.sleep(1)
    location = earth if location==underworld else underworld
    cycle += 1
    if cycle>10: break
```

It was actually Ascalapus who informed Pluto (the god of death, not the cartoon dog, just to be clear.).
I'm not sure why he would do that, why not let the lady eat a few pomegranate seeds? And that's why we
have winter.

### Changing the marks of cattle

Autolycus was a famous thief -- he stole the cattle of Sisyphus, who was a nasty character himself, more
on him later, and changed their identifying marks.

Normally, if we compare the cow objects, they will be compared by their `id` which represents the
location of the object in memory:

```python
class Cow: pass

cow1, cow2 = Cow(), Cow()
print(id(cow1), id(cow2))

cow1 == cow1  # True
cow1 == cow2
```

Ancient sources are a little hazy, but Sysiphus probably changed the identifying mark of the cows in this
way.

```python
class Cow:
    id = None

    def __eq__(self, other):
        return self.id == other.id

    cow1, cow2 = Cow(), Cow()
    cow1.id = 1
    cow2.id = 2
    my_cows = [1,2]
```

And Autolycus simply changed them up after the cow rustling was done:

```python
cow1.id = 125
cow2.id = 126
```

### Icarus Flight

```python
class Wings:
    integrity = 100

    def use(self, temp):
        if temp > 135:
            self.integrity -= 10

class Icarus:
    altitude = 0
    alive = True

    def fly(self):
        temp = 65 + self.altitude * 0.001
        self.wings.use(temp)
        self.altitude += 100
        if self.wings.integrity <= 70:
            self.fall()

    def fall(self):
        if self.altitude > 10000:
            self.alive = False
            print(f'{self} fell at {self.altitude} and died')

icarus = Icarus()
icarus.wings = Wings()
for _ in range(10000):
    if icarus.alive:
        icarus.fly()
```

Icarus, in his arrogance, tried flying higher and higher, closer and closer to the sun and eventually the
beeswax used to secure his wingsuit disintegrated (I'm not sure beeswax is a suitable material in any
case, so it might have disintegrated simply from the mechanical wear during the first flight). But going
along with the legend, and knowing that beeswax melts at 145 degrees (at higher Temperature than
petroleum based wax), I would guess that structural integrity starts to break down at the temperature of
at most 135 degrees, and I will use that number here.

It's interesting that the father of Icarus, Daedalus, was a famous inventor who killed Talos, his nephew,
out of jealousy when he was beginning to prove to be as good (or better) of an inventor as Daedalus, in a
kind of a call-back to the apocryphal jealousy of Salieri for Mozart. I have to wonder if Talos was still
alive and Daedalus was able to run his design by a second set of eyes, that it could have pointed the
material flaws of wax in wingsuit design.

In the same way, Salieri might have garnered much musical inspiration from Mozart if he wasn't so bent on
trying to destroy his rival (although this story is not actually true).


### Friends, Romans, countrymen, Argives, Achaeans, Danaans!

I was always a bit confused about the Homer's use of Achaeans and Danaans, and only in writing this guide
I have found the surprising fact that Homer used the names Achaeans, Danaans and Argives with apparent
impartiality to refer to all Greeks.

```python
class Hellenes: pass

argives = Hellenes()
achaeans = argives
danaans = argives
argives == achaeans == danaans      # True
```

### A rose by a different name...

Dirae or Furiae were daughters of Acheron and Nyx. Some legends maintain they were called Furies in Hell,
Harpies on Earth, and Dirae in Heaven.

```python
class Furiae: pass

furiae = Furiae()

class Hell:
    furies = furiae

class Earth:
    harpies = furiae

class Heaven:
    dirae = furiae
```

Each class creates a new namespace. Names created in the namespace only have significance in that
namespace (and also in enclosed namespaces). So you might get a response of "Dirae who??" outside of
Heaven, but if there was a smaller namespace within heaven, like a small town, the towns-people would
know who Dirae are because from the perspective, Heaven is an outer namespace.


### Apple of Discord

Eris was the goddess of discord who rolled the infamous apple of discord across the floor at the wedding
of Peleus and Thetis. The apple was marked "for the fairest". But who is the fairest? Three attractive
goddesses entered into the contest and Paris (why Paris?) was selected to judge them.

First of all let me say that the ratings below are for illustration only to be used in this guide and not
meant to offend anyone.  I don't wish to be punished if the goddesses are real, in that case please
consider the ratings null and void.

Aside from that, it's not clear if Paris judged the goddesses in earnest and not just based on the gifts
(let's be frank, bribes) that were offered. I'll give him the benefit of the doubt and assume he was just
a big fan of sensual beauty. You can use the famous statues of these goddesses for reference and decide
for yourself.

```python
class Athene:
    sensual_beauty = 7
    solemn_beauty = 10
    power = 7

class Aphrodite:
    sensual_beauty = 10
    solemn_beauty = 7
    power = 7

class Hera:
    sensual_beauty = 7
    solemn_beauty = 7
    power = 10

aphrodite, athene, hera = Aphrodite(), Athene(), Hera()

class Paris:
    def judge(self):
        lst = [athene, aphrodite, hera]
        def order_by(obj):
            return obj.sensual_beauty
        lst.sort(key=order_by, reverse=True)
        return lst[0]

paris = Paris()
winner = paris.judge()
print('The Winner is', winner)
```


### The danger of being too good... at disguising yourself

Dymas was a trojan disguised in armor taken from a dead Greek, accidentally killed by other trojans.

IFF is a military technology used to identify enemies, in the ancient days it typically used the armor,
weapons, hairstyles and so forth, as the uniforms came much later.

```python
from dataclasses import dataclass

@dataclass
class Armor:
    is_greek = False
    is_trojan = False

class Trojan:
    armor = None

    def id(self, other):
        if other.armor.is_greek:
            self.fight(other)

    def fight(self, other):
        print(f'Fighting {other}')

trojan1 = Trojan()
dymas = Trojan()
trojan1.armor = Armor(is_trojan=True)
dymas.armor = Armor(is_greek=True)
trojan1.id(dymas)
```

### Trojan Wooden Horse

Epeus was the designer and builder of the famous horse used to trick the Trojans. This is a good
illustration of the distinction between the class and the object created from class.

At first Epeus created a design of the horse, probably in the form of a blueprint. This is similar to a
class; once he was satisfied with the design, Epeus used it to build the actual wooden horse. The
blueprint and the real thing are completely different -- if the Greeks made the mistake and left the
blueprint at the gates of Illium, it would be a complete disaster (for them, but for Trojans it would be
salvation), -- Trojans would be forewarned by examining the blueprint and the siege would fail
pathetically.

```python
class WoodenHorse: pass

real_wooden_horse = WoodenHorse()
```

### Erigone

Erigone was a daughter of Icarius, who hanged herself when she learned that her father had been killed by
drunken shepherds.

This is an illustration of how an object can accept itself as an argument to an action:

```python
class Erigone:
    def kill(self, other):
        other.die()

    def die(self):
        print(f'{self} died')

erigone = Erigone()
erigone.kill(erigone)
```

This reminds me of a nice story of Erisichthon who derided and offended Demeter (don't do that -- do you
see where this is going?), by cutting down trees in her sacred grove. In revenge, she cursed him with
such insatiable hunger that at last he ate his own legs, and eventually consumed himself completely.

```python
class Erisichthon:
    r_leg = l_leg = True
    body = True

    def __init__(self, places, loc):
        self.places, self.loc = places, loc
        self.places[self.loc] = self

    def super_hunger_eat(self):
        if self.r_leg:
            print('ate right leg')
            self.r_leg = False
        elif self.l_leg:
            print('ate left leg')
            self.l_leg = False
        elif self.body:
            print('ate body')
            self.body = False
        else:
            print('disappear entirely')
            self.places[self.loc] = None

places = [None, None, None]
erisichthon = Erisichthon(places, 0)
for _ in range(4):
    erisichthon.super_hunger_eat()
print(places)
```

### Erulus and his triple arms

Erulus was a son of Feronia, goddess of orchards and woods (my favorite goddess) -- at his birth his
mother had given him three lives and triple arms (that is a fetching look). Evander had to kill him 3
times the same day.

```python
class Evander:
    def kill(self, other):
        other.die()

class Erulus:
    lives = 3
    def die(self):
        if lives:
            print('live another day!')
            lives -= 1
        else:
            print(f'{self} dies')
```


I've used a list of places to represent some potential location where Erisichthon may be, and when he is
completely consumed, Erisichthon removes himself.

### Girdle of Venus

AKA Cestus, this "girdle" (scanty drapery) gave any goddess or mortal woman who wore it the power of
exciting love.

```python
class Cestus: pass

class Girl:
    girdle = None
    base_beauty = 20

    def beauty(self):
        base = self.base_beauty
        if isinstance(self.girdle, Cestus):
            base = base*2 + 5
        return base
girl = Girl()
print('girl beauty', girl.beauty())
girl.girdle = Cestus()
print('girl beauty', girl.beauty())
```

### Call me No Man

Polyphemus was menacing Odysseus and his band, devouring two of them. Odysseus famously used a clever
ruse by calling himself "No man", in order that the other cyclops misinterpret it to mean Nobody (or the
Python value `None`), rather than the Python text string "None":

```python
name = None
if not name:
    print('Stop whining, Polyphemus! You have nobody to blame but yourself.')
name = 'None'
if name:
    print('We shall help you fight your crafty foe, Polyphemus!')
```
