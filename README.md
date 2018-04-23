# Exemples d'utilisation d'expressions régulières en JavaScript

> On parle souvent de regex ou regexp pour parler d'expressions régulières

Par exemple je veux tester une qu'une chaîne contient un nom de domaine.
On va simplifier pour l'instant, et dire qu'un nom de domaine ne comptient que des lettres, un point, puis encore deux ou trois lettres.

L'expression régulière, inspirée du tuto référencé dans la quête, s'écrit.

    [a-z]+\.[a-z]{2,3}

On peut la décomposer en 3 parties :
1. `[a-z]+` indique qu'on veut trouver au moins une lettre minuscule. 
2. Ensuite on veut trouver le caractère point `.`, mais comme c'est un caractère spécial pour les regex, on est obligé de "l'échapper" en ajoutant un `\` avant, ce qui donne `\.`. 
3. Ensuite on cherche au minimum 2, au maximum 3 lettres minuscules avec `[a-z]{2,3}`

**En JavaScript**, pour tester qu'une chaîne est conforme à une expression régulière, on écrit cela :

    regex.test(stringToTest)

On peut écrire la regex soit avec la syntaxe `/regex/`, soit avec `new RegExp('regex')`.

Exemple 1 avec l'expression pour reconnaître un nom de domaine, donnée ci-dessus:

    const regexDomaine = /[a-z]+\.[a-z]{2,3}/
    console.log('google.fr est un nom de domaine?', regexDomaine.test('google.fr'))
    console.log('reactjs.org est un nom de domaine?', regexDomaine.test('reactjs.org'))
    console.log('mydomain.o est un nom de domaine?', regexDomaine.test('reactjs.org'))

Exemple 2 avec une expression (simplifiée) pour reconnaître un email :

    [a-z0-9.]+\@[a-z]+\.[a-z]{2,3}

Décomposons :

1. `[a-z0-9.]+` va matcher les lettres minuscules, les chiffres, et le point `.` (dans les crochets `[]` on n'a pas besoin d'échapper les caractères spéciaux)
2. L'arobase `@` n'a pas besoin d'être échappé (ce n'est pas un caractère spécial)
3. `[a-z]+\.[a-z]{2,3}` est la regex du nom de domaine vue avant

    const regexEmail = /[a-z.]+@[a-z]+\.[a-z]{2,3}/
    console.log('google.fr est une adresse email?', regexEmail.test('google.fr'))
    console.log('joe@google.fr est une adresse email?', regexEmail.test('joe@google.fr'))
    console.log('captain.america@avengers.com est une adresse email?', regexEmail.test('captain.america@avengers.com'))
    console.log('captain.america#avengers.com est une adresse email?', regexEmail.test('captain.america#avengers.com'))

Exemple 3 avec la syntaxe `new Regexp()` et l'expression `^[0-9]{1,2} [A-Za-z]+ [0-9]{4}` qui permet de matcher une date en toutes lettres comme `23 avril 2018`.

Décomposition de la regex:
1. Le caractère `^` permet d'exiger que la chaîne à tester *commence par* ce qui vient après.
2. `[0-9]{1,2}` spécifie 1 ou 2 chiffres. Donc la combinaison `^[0-9]{1,2}` indique qu'on veut avoir un ou deux chiffres au début de la chaîne.
3. Ensuite on exige un espace ` `.
4. Ensuite un nom de mois en toutes lettres (majuscules ou minuscules) avec `[A-Za-z]+`
5. Un autre espace ` `
6. Une année en 4 chiffres avec `[0-9]{4}`

    // Syntaxe new RegExp()
    const regexDate = new RegExp('^[0-9]{1,2} [A-Za-z]+ [0-9]{4}')
    // C'est exactement la même chose que de mettre des //
    const regexDateLitterale = /^[0-9]{1,2} [A-Za-z]+ [0-9]{4}/

    console.log('23 avril 2018 est une date?', regexDate.test('23 avril 2018'))
    console.log('21 janvier 218 est une date?', regexDate.test('21 janvier 218'))
    console.log('231 janvier 2022 est une date?', regexDateLitterale.test('231 janvier 2022'))
