(() => {
    const parsed = JSON.parse(decodeURIComponent(escape(atob(data))));
 
    const answers = parsed.d.sl.g.reduce((first, theme) => {
        const third = theme.S.reduce((second, question) => {
            try {
                const right = question.C.chs.filter(option => option.c);
                const description = question.D.d[0];
 
                if (second[description]) {
                    second[description] = second[description].concat(right.map(option => option.t.d[0]));
                } else {
                    second[description] = right.map(option => option.t.d[0]);
                }
            } catch (_) {}
 
            return second;
        }, {})
 
        return { ...first, ...third };
    }, {});
 
    console.log(answers);
 
    setInterval(() => {
        try {
            const currentQuestionContainers = Array.from(document.querySelectorAll('.player-shape-view span')).filter(el => Object.keys(answers).some(option => option === el.textContent));
 
            const questions = answers[currentQuestionContainers[0].textContent];
 
            Array.from(document.querySelectorAll('.player-shape-view span'))
                .filter(el => questions.some(option => option === el.textContent))
                .map(el => el.textContent.includes('!') || (el.innerText = el.textContent + '!'))
        } catch (_) {}
    }, 5000)
})();