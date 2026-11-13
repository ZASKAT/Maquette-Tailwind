# Tailles et espacements en Tailwind

Fiche mémo pour comprendre les `p-`, `m-`, `gap-`, `w-`, `text-`… avec des exemples tirés de la maquette Fleurs Roussel.

---

## 1. La règle de base : 1 = 4 px

En Tailwind, les nombres **ne sont pas des pixels**. Chaque unité vaut **4 px** (0,25 rem).

| Classe | Calcul | Résultat |
|---|---|---|
| `p-1` | 1 × 4 | 4 px |
| `p-2` | 2 × 4 | 8 px |
| `p-3` | 3 × 4 | 12 px |
| `p-4` | 4 × 4 | **16 px** |
| `p-5` | 5 × 4 | 20 px |
| `p-6` | 6 × 4 | 24 px |
| `p-8` | 8 × 4 | 32 px |
| `p-10` | 10 × 4 | 40 px |
| `p-12` | 12 × 4 | 48 px |
| `p-16` | 16 × 4 | 64 px |
| `p-20` | 20 × 4 | 80 px |
| `p-24` | 24 × 4 | 96 px |

> **Piège classique :** `p-4` ne fait **pas** 4 px, il fait 16 px.

### Passer de Figma à Tailwind

Dans Figma, tu lis une valeur en pixels. **Divise-la par 4** :

- Figma affiche 24 px → `24 ÷ 4 = 6` → `p-6`
- Figma affiche 40 px → `40 ÷ 4 = 10` → `p-10`
- Figma affiche 18 px → `18 ÷ 4 = 4,5` → `p-4.5` (les demi-valeurs existent)

En Tailwind v4, **tous les nombres entiers fonctionnent** : `p-7`, `p-13`, `p-15`… même s'ils ne sont pas dans le tableau.

Si la valeur ne tombe vraiment pas juste, tu peux écrire une **valeur exacte** entre crochets :

```html
<div class="p-[18px]">…</div>
```

À utiliser avec modération : les valeurs de l'échelle rendent le site plus régulier.

---

## 2. Padding, margin et gap : qui fait quoi ?

```
┌──────────── margin (m-) : espace À L'EXTÉRIEUR ────────────┐
│  ┌──────────── bordure ─────────────────────────────────┐  │
│  │  padding (p-) : espace À L'INTÉRIEUR                 │  │
│  │     ┌────────────────────────────┐                   │  │
│  │     │         contenu            │                   │  │
│  │     └────────────────────────────┘                   │  │
│  └──────────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────────┘
```

| Préfixe | Rôle | Quand l'utiliser |
|---|---|---|
| `p-` | **padding** : espace entre le bord et le contenu | Donner de l'air à l'intérieur d'un bouton, d'une carte, d'une section |
| `m-` | **margin** : espace autour de l'élément | Écarter un élément de celui d'au-dessus (`mt-4`) |
| `gap-` | espace **entre les enfants** d'un `flex` ou d'une `grid` | Espacer des cartes, des colonnes, des boutons côte à côte |
| `space-y-` | espace vertical entre les enfants (hors flex/grid) | Espacer les éléments d'une liste `<ul>` |

> **Astuce :** quand des éléments sont dans un `flex` ou une `grid`, utilise **`gap`** plutôt que des marges sur chaque enfant. C'est plus simple et il n'y a pas d'espace en trop à la fin.

---

## 3. Choisir le côté : x, y, t, r, b, l

La même logique marche pour `p-` et `m-` :

| Classe | Côtés concernés | Exemple |
|---|---|---|
| `p-4` | les 4 côtés | 16 px partout |
| `px-4` | gauche + droite (axe **x**, horizontal) | marges latérales d'une page |
| `py-4` | haut + bas (axe **y**, vertical) | hauteur d'une section |
| `pt-4` | **t**op (haut) | |
| `pr-4` | **r**ight (droite) | |
| `pb-4` | **b**ottom (bas) | |
| `pl-4` | **l**eft (gauche) | |

On peut **combiner** : `px-6 py-3` = 24 px sur les côtés, 12 px en haut et en bas.
C'est exactement le padding des boutons de la maquette :

```html
<a class="rounded-full bg-marque px-6 py-3 text-white">Voir les bouquets</a>
```

Un bouton est presque toujours **plus large que haut** : le `px` est plus grand que le `py`.

---

## 4. Centrer et limiter la largeur d'une page

C'est la combinaison qu'on retrouve dans chaque section de la maquette :

```html
<div class="mx-auto max-w-6xl px-4 md:px-6">
```

| Classe | Rôle |
|---|---|
| `max-w-6xl` | le contenu ne dépasse jamais **1152 px** de large |
| `mx-auto` | marges gauche/droite automatiques → le bloc est **centré** |
| `px-4` | 16 px de chaque côté sur mobile, pour que le texte ne colle pas au bord de l'écran |
| `md:px-6` | 24 px à partir de la tablette |

> **Pourquoi `mx-auto` ne centre pas toujours ?** Il ne marche que si l'élément a une largeur limitée (`max-w-…` ou `w-…`). Sans ça, le bloc prend déjà toute la largeur et il n'y a rien à centrer.

Largeurs maximales utiles :

| Classe | Largeur max |
|---|---|
| `max-w-md` | 448 px |
| `max-w-xl` | 576 px (bien pour un paragraphe) |
| `max-w-3xl` | 768 px |
| `max-w-6xl` | 1152 px (bien pour une page) |
| `max-w-7xl` | 1280 px |

---

## 5. Largeur et hauteur : w, h, size

| Classe | Résultat |
|---|---|
| `w-full` | 100 % de la largeur du parent (images, boutons sur mobile) |
| `w-auto` | largeur naturelle |
| `w-16` | 64 px de large (même échelle × 4) |
| `h-16` | 64 px de haut |
| `size-16` | 64 px de large **et** de haut (pratique pour les ronds et les icônes) |
| `w-1/2` | 50 % du parent |

Exemple dans la maquette, le cercle blanc autour des icônes :

```html
<div class="flex size-16 items-center justify-center rounded-full bg-white">
    <img src="img/icone-saison.svg" alt="" class="size-7">
</div>
```

→ un rond de 64 × 64 px qui contient une icône de 28 × 28 px centrée.

---

## 6. Taille du texte : `text-`

Attention, ici **ce n'est pas l'échelle × 4** : ce sont des noms.

| Classe | Taille | Utilisation dans la maquette |
|---|---|---|
| `text-xs` | 12 px | « ARTISAN FLEURISTE… », copyright |
| `text-sm` | 14 px | menu, descriptions des cartes, footer |
| `text-base` | 16 px | texte normal (valeur par défaut) |
| `text-lg` | 18 px | prix, texte du hero sur desktop |
| `text-xl` | 20 px | titres des cartes, logo mobile |
| `text-2xl` | 24 px | logo desktop |
| `text-3xl` | 30 px | titres de section sur mobile |
| `text-4xl` | 36 px | titre principal sur mobile, titres de section sur desktop |
| `text-5xl` | 48 px | |
| `text-6xl` | 60 px | titre principal sur desktop |

> **Piège :** `text-4xl` n'est pas « 4 fois plus grand », c'est juste un nom.

Classes souvent associées :

| Classe | Rôle |
|---|---|
| `leading-tight` | lignes serrées, idéal pour les **gros titres** |
| `leading-relaxed` | lignes aérées, idéal pour les **paragraphes** |
| `tracking-widest` | lettres très espacées (petits textes en majuscules) |
| `font-medium` / `font-semibold` | épaisseur 500 / 600 |

---

## 7. Arrondis : `rounded-`

| Classe | Rayon | Dans la maquette |
|---|---|---|
| `rounded` | 4 px | |
| `rounded-lg` | 8 px | |
| `rounded-2xl` | 16 px | cartes des bouquets |
| `rounded-3xl` | 24 px | grandes illustrations |
| `rounded-full` | complètement rond | boutons « pilule », cercles des icônes |

---

## 8. Les tailles qui changent selon l'écran (mobile first)

On écrit d'abord la taille **mobile**, puis on la **remplace** pour les écrans plus grands :

```html
<h1 class="text-4xl lg:text-6xl">…</h1>
<section class="py-16 lg:py-24">…</section>
```

| Classe | Mobile | ≥ 768 px (`md:`) | ≥ 1024 px (`lg:`) |
|---|---|---|---|
| `text-4xl lg:text-6xl` | 36 px | 36 px | **60 px** |
| `py-16 lg:py-24` | 64 px | 64 px | **96 px** |
| `px-4 md:px-6` | 16 px | **24 px** | 24 px |

Une valeur reste active **jusqu'à ce qu'un préfixe plus grand la remplace**.

> **Piège :** `md:` veut dire « **à partir de** 768 px », pas « seulement sur tablette ». Une classe sans préfixe s'applique partout, y compris sur desktop.

---

## 9. Méthode quand on bloque

1. **Mesure dans Figma** : clique sur l'élément, puis maintiens `Alt` en survolant un voisin pour voir la distance en pixels.
2. **Divise par 4** pour trouver la classe (`32 px` → `8`).
3. **Demande-toi si c'est de l'espace dedans ou dehors** :
   - dedans → `p-`
   - entre deux éléments frères dans un flex/grid → `gap-`
   - au-dessus d'un élément seul → `mt-`
4. **Vérifie dans le navigateur** : `F12`, puis survole l'élément. Le padding s'affiche en **vert** et la margin en **orange**.
5. **Commence par le mobile**, puis ajoute `md:` / `lg:` seulement si la maquette desktop est différente.

---

## 10. Antisèche express

```
1 unité = 4 px         p-4 = 16 px       p-6 = 24 px       p-8 = 32 px
p  = padding (dedans)   m = margin (dehors)   gap = entre les enfants
x  = gauche + droite    y = haut + bas
t / r / b / l = haut / droite / bas / gauche
mx-auto + max-w-…      = bloc centré
w-full                 = toute la largeur
size-16                = 64 × 64 px
text-sm 14 · base 16 · lg 18 · xl 20 · 2xl 24 · 3xl 30 · 4xl 36 · 6xl 60
sans préfixe = mobile · md: ≥ 768 px · lg: ≥ 1024 px
```

---

## 11. Pourquoi répéter les mêmes classes au lieu de les mettre sur le `<ul>` ?

Dans la section « Pourquoi choisir Fleurs Roussel ? », cette ligne revient 3 fois :

```html
<div class="mx-auto flex size-16 items-center justify-center rounded-full bg-white">
```

On pourrait penser qu'il suffit de l'écrire une fois sur le `<ul>`. **Ça ne marche pas**, pour deux raisons.

### Raison 1 : une classe s'applique à l'élément qui la porte

Ces classes décrivent **le rond blanc autour de chaque icône**. Si on les met sur le `<ul>`, c'est **la liste entière** qui devient le rond :

```html
<!-- ❌ Ce qui se passerait -->
<ul class="mx-auto flex size-16 items-center justify-center rounded-full bg-white">
    <li>…</li>   <!-- les 3 avantages entassés dans un rond de 64 × 64 px -->
    <li>…</li>
    <li>…</li>
</ul>
```

Résultat : un seul petit cercle blanc de 64 px, dans lequel les trois avantages (icône, titre, texte) sont écrasés et débordent.

### Raison 2 : la plupart des propriétés ne se transmettent pas aux enfants

En CSS, seules **certaines** propriétés sont **héritées** par les enfants, principalement celles qui concernent **le texte**.

| Héritées (passent aux enfants) | Non héritées (restent sur l'élément) |
|---|---|
| `text-white`, `text-marque` (couleur) | `bg-white` (fond) |
| `font-titre`, `font-semibold` | `size-16`, `w-…`, `h-…` |
| `text-sm`, `text-xl` (taille) | `p-…`, `m-…`, `mx-auto` |
| `text-center` | `flex`, `items-center`, `justify-center` |
| `leading-…`, `tracking-…` | `rounded-full`, `border-…` |

C'est pour ça que la page utilise `text-center` **sur la section** : il est hérité par tous les titres et paragraphes à l'intérieur, sans le répéter. En revanche, un fond, une taille ou un arrondi doivent être posés **sur l'élément lui-même**.

> **À retenir :** le texte s'hérite, la boîte ne s'hérite pas.

### Est-ce grave de répéter ?

Non, c'est **normal en Tailwind**. La documentation officielle le dit : la répétition est le prix à payer pour voir tout le style directement dans le HTML. Dans un vrai projet, ces 3 blocs seraient générés par une **boucle** (en PHP, JavaScript, React…), et le code ne serait écrit qu'une seule fois.

Astuce VS Code : pour modifier les 3 lignes d'un coup, sélectionne le texte puis appuie sur `Ctrl+D` plusieurs fois (multi-curseur).

### Si on veut vraiment éviter la répétition

**Option A : créer sa propre classe** dans `src/input.css` avec `@apply` :

```css
@layer components {
    .icone-rond {
        @apply mx-auto flex size-16 items-center justify-center rounded-full bg-white;
    }
}
```

```html
<div class="icone-rond">
    <img src="img/icone-saison.svg" alt="" class="size-7">
</div>
```

C'est la bonne solution quand un même « composant » revient souvent (par exemple les boutons). Inconvénient : il faut ouvrir le fichier CSS pour savoir ce que fait `icone-rond`.

**Option B : cibler les enfants depuis le parent** (variante arbitraire) :

```html
<ul class="[&_div]:mx-auto [&_div]:flex [&_div]:size-16 …">
```

`[&_div]:size-16` veut dire « tous les `div` à l'intérieur de moi font 64 px ». Ça fonctionne, mais c'est **plus difficile à lire** que la répétition. À éviter quand on débute.

### En résumé

| Solution | Lisibilité | Quand l'utiliser |
|---|---|---|
| Répéter les classes | ⭐⭐⭐ on voit tout dans le HTML | Peu de répétitions (2 à 4), ou contenu généré par une boucle |
| Classe perso avec `@apply` | ⭐⭐ | Élément réutilisé partout (boutons, cartes) |
| Variante `[&_div]:` | ⭐ | Rarement, quand on ne peut pas toucher aux enfants |
