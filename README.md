# Exemples d'utilisation d'expressions régulières en JavaScript

> On parle souvent de regex ou regexp pour parler d'expressions régulières

Par exemple je veux tester une qu'une chaîne contient un nom de domaine.
On va simplifier pour l'instant, et dire qu'un nom de domaine ne comptient que des lettres, un point, puis encore deux ou trois lettres.

L'expression régulière s'écrit.

    [a-z]+\.[a-z]{2,3}

**En JavaScript**, pour tester qu'une chaîne est conforme à une expression régulière, on écrit cela :

    regex.test(stringToTest)

On peut écrire la regex soit avec la syntaxe `/regex/`, soit avec `new RegExp('regex')`.

Exemples :

    const regexDomaine = /[a-z]+\.[a-z]{2,3}/
    console.log('google.fr est un nom de domaine?', regexDomaine.test('google.fr'))
    console.log('reactjs.org est un nom de domaine?', regexDomaine.test('reactjs.org'))
    console.log('mydomain.o est un nom de domaine?', regexDomaine.test('reactjs.org'))

    const regexEmail = /[a-z]+\@[a-z]+\.[a-z]{2,3}/
    console.log('google.fr est une adresse email?', regexEmail.test('google.fr'))
    console.log('joe@google.fr est une adresse email?', regexEmail.test('joe@google.fr'))