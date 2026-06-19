STEM Learning App Builder ("LA·CORE" pattern)
Converts STEM source material into ONE self-contained HTML file: an interactive, ADHD-friendly course with a guided teach-first flow per concept, gamification, and bionic reading. Works offline and on phones.
THE GOLDEN RULE (read first)
Every lesson's content must be fully readable with JavaScript disabled. When a file is texted/AirDropped and the user just taps it, iOS opens it in Quick Look — a sandboxed preview that paints HTML but freezes JavaScript. So you build TWO layers in the same file:

Static "Reading Mode" — every concept rendered as plain scrollable HTML, baked into the file, bionic baked in at build time, math via the Unicode fallback. Visible by default.
Interactive app — the JS engine (one step at a time, XP, quiz checking, navigation), hidden until JS runs.

JS reveals the app and hides the static layer via the html.js-ready pattern. If JS freezes, the user still reads the full lesson — never a blank screen. Everything marked [HARDENING] exists because of real phone failures. Apply all of it.
What the app contains
Per concept, a 4-step teach-first flow (the question comes LAST, after teaching):

💡 The Idea — a one-line hook (surprising, curiosity-sparking), a "why you should care" payoff box, the plain-English idea, and a real-world analogy.
👁 See It — a simple inline-SVG visual, the formula, and the formula explained piece by piece. Optional tiny no-pressure gut-check (2-option tap) for a dopamine hit.
✍️ Worked Example — a full problem solved step-by-step, every line shown, revealed one step at a time, key numbers color-coded.
🎯 Now You Try — the quiz question with hints + reveal, awards XP. Then a 🔒 Lock it in one-line recap.

Hyperfocus bait (ordering): hyperfocus can't be commanded, only baited. When chunking the source into the LEARN array, flag whichever concept is most surprising or has the strongest hook as `isHookConcept: true` and place it FIRST in the module, regardless of where it sits in the source's own order. That first dopamine hit is what gets the snowball rolling through the drier concepts that follow.

Rabbit Hole (tangent harvesting): going down tangents is part of how this brain engages — the app should let it happen productively instead of forcing strict linear progress. After "Lock it in" on any concept, show an optional small 🐇 "Go deeper?" link that reveals a short bonus card (one extra fact, edge case, or "what if" tied to that concept). Completing the bonus card awards a small XP bonus and returns the learner to the main path — the tangent gets harvested into progress instead of just being a detour.

Gamification (ADHD engagement): XP per correct answer, player levels with rank names, streaks with milestone toasts, confetti on correct, progress bar. Keep rewards frequent (every 30–60s) and varied (rotate praise messages).
Reading aids: bionic reading ON by default + toggle with Light/Medium/Strong intensity; Atkinson Hyperlegible body font; high-contrast dark theme; generous line spacing.
Data model
Extract the source into a LEARN array of modules; each module has concepts; each concept:
javascript{
  title, hook, why, idea, analogy,
  isHookConcept,  // true for the one concept per module placed first to bait hyperfocus
  visual,        // inline SVG string (CSS vars for color; max-width:100%)
  formula, formulaNote,
  gutCheck:{ q, options:[a,b], correct:0|1, explain },   // optional
  worked:{ prompt, steps:[{do, math}], answer },
  tryQ:{ q, eq, answers:[...accepted strings...], hints:[...], explain, diff:1-4 },
  lockin,
  rabbitHole:{ teaser, fact, xpBonus }   // optional — the "Go deeper?" bonus card
}
Math goes in formula/math/eq as LaTeX; prose uses <strong>, <em>, <code>. Put several accepted spellings in tryQ.answers (checker normalizes case/space + prefix/inclusion match).
Build process

Extract the source. PDFs: pdftotext page-by-page, pdfimages for figures. Slides: use the pptx skill to read them.
Chunk into concepts — ONE idea per card. Keep small (ADHD pacing). For each module, flag the single most surprising/curiosity-sparking concept as `isHookConcept` and order it first.
Author each concept's fields. For STEM, the worked example is the heart — show real step-by-step math/derivation, not just prose. Write genuine analogies (dot product = pushing a shopping cart; derivative = a speedometer).
Generate the HTML with BOTH layers (static reading + interactive app).
Harden (all techniques below).
Output one .html to /mnt/user-data/outputs/, present with present_files.


[HARDENING] 1. Progressive enhancement (never blank)
html<body>
  <div id="appRoot">...interactive UI...</div>
  <div id="staticContent">...FULL readable lessons baked in...</div>
</body>
css#staticContent{display:block}
#appRoot{display:none}
html.js-ready #staticContent{display:none}
html.js-ready #appRoot{display:flex}
javascript(function init(){
  try{
    document.documentElement.className += ' js-ready'; // FIRST: reveal app, hide static
    /* ...setup... */
  }catch(err){
    // revert to static so content is never lost
    document.documentElement.className = document.documentElement.className.replace(' js-ready','');
  }
})();
window.addEventListener('error',function(){
  try{
    if(document.documentElement.className.indexOf('js-ready')>=0){
      var c=document.getElementById('content');
      if(c && c.innerHTML.trim().length<20)
        document.documentElement.className = document.documentElement.className.replace(' js-ready','');
    }
  }catch(e){}
});
[HARDENING] 2. Robust string-based bionic (apply to BOTH layers)
NEVER walk the DOM at runtime (createTreeWalker) — it breaks in preview, double-applies, and bolds math/code. Use this string transform on prose strings BEFORE inserting (interactive layer) and at build time (static layer). A past bug was hardening the static layer but forgetting bionic in it — apply to both.
javascriptfunction bionicWord(w){
  var m=w.match(/^([^A-Za-z]*)([A-Za-z]+)([\s\S]*)$/); if(!m)return w;
  var n=Math.max(1,Math.round(m[2].length*0.45)); // 0.33 light / 0.45 med / 0.6 strong
  return m[1]+'<b class="bx">'+m[2].slice(0,n)+'</b>'+m[2].slice(n)+m[3];
}
function bionicHTML(html){
  if(html==null)return '';
  var math=[];
  var s=String(html)
    .replace(/\\\([\s\S]*?\\\)/g,function(x){math.push(x);return '\u0000'+(math.length-1)+'\u0000';})
    .replace(/\\\[[\s\S]*?\\\]/g,function(x){math.push(x);return '\u0000'+(math.length-1)+'\u0000';})
    .replace(/\$\$[\s\S]*?\$\$/g,function(x){math.push(x);return '\u0000'+(math.length-1)+'\u0000';});
  var parts=s.split(/(<[^>]+>)/g);
  var OPEN=/^<\s*(code|pre|script|style|svg|b|mjx)/i, CLOSE=/^<\s*\/\s*(code|pre|script|style|svg|b|mjx)/i;
  var skip=0,out='';
  parts.forEach(function(p){
    if(!p)return;
    if(p[0]==='<'){ if(CLOSE.test(p))skip=Math.max(0,skip-1); else if(OPEN.test(p)&&!/\/>\s*$/.test(p))skip++; out+=p; }
    else { out+= skip>0 ? p : p.replace(/\S+/g,function(w){return w.indexOf('\u0000')>=0?w:bionicWord(w);}); }
  });
  return out.replace(/\u0000(\d+)\u0000/g,function(_,i){return math[+i];});
}
Toggle with CSS, never by re-running: body:not(.bionic-on) .bx{font-weight:normal} (or default ON and let the toggle remove it).
[HARDENING] 3. Guard every MathJax call
window.MathJax is truthy as soon as the config exists, but .typesetPromise isn't ready until the library loads. Always:
javascriptif(window.MathJax && window.MathJax.typesetPromise) MathJax.typesetPromise([el]).catch(function(){});
[HARDENING] 4. LaTeX → Unicode fallback (for the static layer)
So equations are legible even when MathJax never loads (offline/preview). MathJax upgrades them if it loads.
javascriptfunction latexToUnicode(s){
  if(!s)return '';
  var t=String(s).replace(/\\\[|\\\]|\\\(|\\\)|\$\$|\$/g,'');
  t=t.replace(/\\sqrt\s*\{([^}]*)\}/g,'√($1)').replace(/\\sqrt\s*(\w)/g,'√$1');
  t=t.replace(/\\frac\s*\{([^}]*)\}\s*\{([^}]*)\}/g,'($1)/($2)');
  t=t.replace(/\\sum/g,'∑').replace(/\\prod/g,'∏').replace(/\\int/g,'∫').replace(/\\in\b/g,'∈');
  t=t.replace(/\\times/g,'×').replace(/\\cdot/g,'·').replace(/\\pm/g,'±').replace(/\\to|\\rightarrow/g,'→');
  t=t.replace(/\\leq/g,'≤').replace(/\\geq/g,'≥').replace(/\\neq/g,'≠').replace(/\\approx/g,'≈').replace(/\\infty/g,'∞').replace(/\\nabla/g,'∇').replace(/\\partial/g,'∂');
  t=t.replace(/\\alpha/g,'α').replace(/\\beta/g,'β').replace(/\\gamma/g,'γ').replace(/\\delta/g,'δ').replace(/\\theta/g,'θ').replace(/\\lambda/g,'λ').replace(/\\mu/g,'μ').replace(/\\sigma/g,'σ').replace(/\\Sigma/g,'Σ').replace(/\\pi/g,'π').replace(/\\phi/g,'φ').replace(/\\omega/g,'ω');
  t=t.replace(/\\mathbb\{R\}/g,'ℝ').replace(/\\mathbb\{([A-Z])\}/g,'$1').replace(/\\mathbf\{([^}]*)\}/g,'$1').replace(/\\text\{([^}]*)\}/g,'$1');
  t=t.replace(/\\begin\{[^}]*\}|\\end\{[^}]*\}/g,'').replace(/\\\\/g,'; ').replace(/&/g,' ').replace(/\\color\{[^}]*\}/g,'').replace(/\\\|/g,'‖');
  var sup={'0':'⁰','1':'¹','2':'²','3':'³','4':'⁴','5':'⁵','6':'⁶','7':'⁷','8':'⁸','9':'⁹','n':'ⁿ','i':'ⁱ','+':'⁺','-':'⁻','T':'ᵀ'};
  t=t.replace(/\^\{([^}]*)\}/g,function(m,g){return g.split('').map(function(c){return sup[c]||c;}).join('');}).replace(/\^(\w)/g,function(m,g){return sup[g]||'^'+g;});
  var sub={'0':'₀','1':'₁','2':'₂','3':'₃','4':'₄','5':'₅','6':'₆','7':'₇','8':'₈','9':'₉','i':'ᵢ','j':'ⱼ','n':'ₙ','+':'₊','-':'₋'};
  t=t.replace(/_\{([^}]*)\}/g,function(m,g){return /^[0-9ijn+\-]+$/.test(g)?g.split('').map(function(c){return sub[c]||c;}).join(''):'('+g+')';}).replace(/_(\w)/g,function(m,g){return sub[g]||'_'+g;});
  return t.replace(/[{}]/g,'').replace(/\s+/g,' ').trim();
}
// e.g. \sum_{i=1}^{4} i → ∑(i=1)⁴ i ;  \sqrt{v_1^2+v_2^2} → √(v₁²+v₂²) ;  \mathbf{v}\in\mathbb{R}^3 → v∈ℝ³
[HARDENING] 5. Mobile layout

<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, maximum-scale=5.0">
Sidebar → slide-out drawer behind a ☰ button at @media (max-width:760px); never a fixed 280px panel.
max-width:100% on images/SVGs; tap targets ≥44px; -webkit-tap-highlight-color:transparent.
Inputs/buttons full-width on mobile; multi-option rows stack vertically.
-webkit-overflow-scrolling:touch on scroll containers; no hover-only interactions.
Verify no overflow at 380px.


Before delivering — verify

 Every concept readable with JavaScript disabled (static Reading Mode never blank)
 Bionic present in BOTH the interactive and static layers
 Every MathJax call guarded with && window.MathJax.typesetPromise
 Math has a Unicode fallback in the static layer
 No horizontal overflow at 380px; sidebar is a drawer on mobile; tap targets ≥44px
 Quiz answer-checking accepts reasonable variants
 XP / level / streak / confetti fire on correct answers
 Each module opens on its flagged hook concept, not source order
 Rabbit Hole bonus cards (where present) award XP and return cleanly to the main path
 After "Lock it in" on any math-heavy concept, offer the fluency drill handoff (see below)

## Math Fluency Drill Handoff
After completing the 🔒 Lock it in step on any concept involving formulas, equations, or computation, show:

```
🔢 Want to drill this with practice problems?
Type "drill me" to build procedural fluency on [concept name].
```

Do NOT auto-switch. Wait for user confirmation.
If yes → hand off to math-fluency-drill with: course name, lesson number, concept name.
If no → continue to next concept normally.
