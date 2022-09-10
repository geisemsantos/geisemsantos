fRealizaConversao = (comprimento, tipoInicial, tipoFinal) => {
    if (tipoInicial == 'M' && tipoFinal == 'KM') {
        return comprimento/1000;
    }
    if (tipoInicial == 'M' && tipoFinal == 'CM') {
        return comprimento*100;
    }
    if (tipoInicial == 'M' && tipoFinal == 'MM') {
        return comprimento * 1000;
    }
    if (tipoInicial == 'KM' && tipoFinal == 'M') {
        return comprimento * 1000;
    }
    if (tipoInicial == 'KM' && tipoFinal == 'CM') {
        return comprimento * 100000
    }
    if (tipoInicial == 'KM' && tipoFinal == 'MM') {
        return comprimento* 1000000;
    }
    if (tipoInicial == 'CM' && tipoFinal == 'M') {
        return comprimento/100;
    }
    if (tipoInicial == 'CM' && tipoFinal == 'KM') {
        return comprimento / 100000;
    }
    if (tipoInicial == 'CM' && tipoFinal == 'MM') {
        return comprimento * 10;
    }
    if (tipoInicial == 'MM' && tipoFinal == 'M') {
        return comprimento/1000;
    }
    if (tipoInicial == 'MM' && tipoFinal == 'KM') {
        return comprimento /1000000;
    }
    if (tipoInicial == 'MM' && tipoFinal == 'CM') {
        return comprimento/ 10;
    }
    
    if (tipoInicial == tipoFinal) {
        return context.res.status(400).send('Formato de dado incorreto, o campo inicial precisa ser diferente do final');
    }

    };

module.exports = async function (context, req) {
    let comprimento = Number(req.query.comprimento);
    let tipoInicial = String(req.query.tipoInicial);
    let tipoFinal = String(req.query.tipoFinal);
    
    if (isNaN(comprimento)) {
        return context.res.status(400).send('Formato de dado incorreto, o campo comprimento aceita somente numeros.');
    }

     let resultado = fRealizaConversao(comprimento, tipoInicial, tipoFinal);

    context.res.json({
        comprimento: comprimento, 
        inical: tipoInicial, 
        final: tipoFinal, 
        resultado: resultado
    });
}
