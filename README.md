```
(() => {
    const normalize = str => str.replace(/\s+/g, ' ').trim();

    const parsed = JSON.parse(decodeURIComponent(escape(atob(data))));

    const answers = parsed.d.sl.g.reduce((first, theme) => {
        const third = theme.S.reduce((second, question) => {
            try {
                const right = question.C.chs.filter(option => option.c);
                const description = normalize(question.D.d[0].split('\n')[0]);

                if (second[description]) {
                    second[description] = second[description].concat(
                        right.map(option => normalize(option.t.d[0]))
                    );
                } else {
                    second[description] = right.map(option => normalize(option.t.d[0]));
                }
            } catch (_) {}

            return second;
        }, {})

        return { ...first, ...third };
    }, {});

    console.log(answers);

    setInterval(() => {
        try {
            const allSpans = Array.from(document.querySelectorAll('.player-shape-view span'));

            const currentQuestionContainers = allSpans.filter(el =>
                Object.keys(answers).some(key => key === normalize(el.textContent))
            );

            if (!currentQuestionContainers.length) return;

            const questions = answers[normalize(currentQuestionContainers[0].textContent)];
            allSpans
                .filter(el => questions.some(option => option === normalize(el.textContent)))
                .forEach(el => {
                    if (!el.textContent.includes('!')) {
                        el.innerText = el.textContent + '!';
                    }
                });
        } catch (_) {}
    }, 5000);
})();
```



```
-d1 -d3+s -s6+s -d9+s -s12+s -d15+s -s20+s -d25+s -s30+s -d35+s -r1+s -S -a1 -As -d1 -d3+s -s6+s -d9+s -s12+s -d15+s -s20+s -d25+s -s30+s -d35+s -S -a1
```