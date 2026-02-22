# aureum-website-2-import { useState, useEffect, useRef, useCallback } from "react";
import { AreaChart, Area, XAxis, YAxis, Tooltip, ResponsiveContainer, PieChart, Pie, Cell, CartesianGrid } from "recharts";

/* â•â•â• FONTS â€” v16: Service detail modals, FT quarterly report, bank directory, cleaner language/access sections â•â•â• */
const FU = "https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;0,700;1,400&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&display=swap";

/* â•â•â• i18n â•â•â• */
const T = {
en:{
  nav:["Services","Process","Preview","About","Pricing","Get Started"],
  hero_lab:"The World's Best Private Bankers. In Your Language.",
  hero_h:["Access the world's leading banks. ","Lower your costs. ","Understand your wealth."],
  hero_p:"We connect you with top private bankers across 25+ international banksâ€”matching you with bankers who speak your language. Then we reduce your total costs, create clear reporting, and benchmark your portfolio against peers.",
  hero_fq:"\u201CEvery serious investor deserves access to global banking, transparent costs, and independent analysis.\u201D",hero_fqa:"\u2014 Noah Kraama, Founder",
  hero_cta:["Start Your Search","See How It Works"],
  stats:[["18+ Years","Wealth Heritage"],["0%","Commissions or Kickbacks"],["25+","Global Banks"],["Up to 15","Proposals Per Search"]],
  svc_lab:"What We Do",svc_h:"Global access. Lower costs. Clear reporting. Advanced analysis.",
  svcs:[
    ["Access Top Bankers Worldwide","We connect you with the world's leading private banksâ€”from Zurich to Singapore. We find bankers who speak your language: Finnish, Swedish, or English. You meet them. You choose.","Up to 15 proposals"],
    ["Reduce Your Total Costs","We identify every fee layer your bank chargesâ€”including hidden costs like FX spreads and fund fees. Through collective negotiating power, we reduce your total costs by an average of 0.50%.","Ongoing savings"],
    ["Benchmark Your Portfolio","Clear monthly reports in your language. Peer-to-peer comparisons. Monte Carlo simulations. Stress testing. Advanced risk analysis. See how your portfolio actually performs against relevant benchmarks.","Monthly reporting"],
    ["Always Available Insights","Message us about markets or your portfolioâ€”WhatsApp, Telegram, or Signal. Get clear answers based on your latest data. No newsletters. No noise.","24/7 access"]],
  lang_lab:"Your Language",lang_h:"Discuss your wealth in Finnish, Swedish or English",
  lang_p1:"We find Finnish and Swedish-speaking bankers at the world's top international banks. Geneva, Luxembourg, Singaporeâ€”in your mother tongue.",
  lang_p2:"All reports and communication in Finnish, Swedish, or English.",
  langs:[["Suomeksi","Finnish-speaking bankers at international banks","\"I chose a Finnish private bank with institutional-grade service. Having everything in Finnishâ€”from reports to meetingsâ€”changed how I engage with my wealth.\"","â€” T.L., Entrepreneur, Helsinki"],["PÃ¥ svenska","Swedish-speaking relationship managers worldwide","\"Found a Swedish-speaking banker in Luxembourg who understands Nordic business culture. Finally feel properly understood.\"","â€” M.S., Family Office, Turku"],["In English","Full access to global banking network","\"Aureum connected me with a banker in Singapore who covers both European and Asian markets. Seamless English communication throughout.\"","â€” J.K., Tech Investor, Espoo"]],
  hw_lab:"How It Works",hw_h:"Four simple steps",
  steps:[
    ["Tell Us Your Needs","5-minute conversation about your portfolio, language preference, and what matters to you. We identify which banks and jurisdictions fit.","5 minutes"],
    ["Meet the Bankers","We send your profile to 25+ banks. You receive up to 15 proposals. We arrange meetings with bankers who speak your language.","2 weeks"],
    ["Choose Your Bank","Compare proposals side by side. Meet the bankers. You decide who manages your wealth.","Your pace"],
    ["Lower Costs, Better Reporting","We reduce your total costs and create clear monthly reports. Benchmark your portfolio. Message us anytime.","Ongoing"]],
  /* v13: Social proof */
  sp_lab:"Real Results",sp_h:"â‚¬2.3M portfolio â€” 34% lower total costs",
  sp_intro:"Finnish tech entrepreneur. 8 years with one Swiss bank. Never compared alternatives. Total costs: 1.45%. After Aureum: 12 proposals. Finnish-speaking banker found. New total costs: 0.95%. That's 34% less. See the long-term impact in our calculator below.",
  sp_steps:[
    ["Day 1","Shared his profile with Aureum. Five-minute onboarding conversation.","\u2713"],
    ["Day 3","Anonymized profile sent to 15 banks across 4 jurisdictions.","\u2192"],
    ["Day 12","12 proposals received. Three banks had Finnish-speaking relationship managers.","\u25C8"],
    ["Day 18","Met four bankers via video. One in-person meeting in Geneva.","\u25A3"],
    ["Day 25","Selected a new bank. All-in costs dropped from 1.45% to 0.95%.","\u2B25"]],
  sp_results:[["12","Proposals received"],["0.50%","Fee reduction"],["Finnish","Speaking banker found"],["â‚¬2.3M","Under monitoring"]],
  sp_note:"Names and details anonymized. Aureum does not provide investment advice. All decisions were made by the client.",

  prev_lab:"See it in Action",prev_h:"This is what your reporting could look like",prev_tabs:["Bespoke Report","WhatsApp Insights"],
  portal_lab:"Client Portal",portal_h:"How you see your wealth. Always current.",
  fdr_lab:"The Founder",fdr_name:"Noah Kraama",fdr_title:"Founder \u00B7 Aureum Private Office",art_lab:"From the Founder\u2019s Desk",
  fdr_q:"Global banking should not be reserved for the ultra-wealthy.",
  fdr_quotes:[
    "You deserve access to the world's best bankersâ€”regardless of where you live or what language you speak.",
    "Banks rarely disclose total costs. We make every fee visible. Then we negotiate better terms.",
    "From â‚¬250,000, you get the same quality of reporting and analysis that billionaires receive."
  ],
  fdr_bio:[
    "Noah Kraama's parents are both Finnish. He was born in the United States and spent his childhood in JyvÃ¤skylÃ¤ and Helsinki, but has lived most of his life in Luxembourg. His mother tongue is Finnish, and he speaks English, French, Luxembourgish, and some German and Spanish.",
    "His father spent nearly two decades at one of Switzerland's most established private banking institutions, advising some of the wealthiest Finnish families and investors from Luxembourg. His mother built her career in institutional private equity, where governance frameworks and mandate discipline are foundational.",
    "Growing up at this intersection revealed a structural gap. Institutional investors benchmark systematicallyâ€”they renegotiate custody agreements, quantify total cost layers, and reassess structures as conditions evolve. Private investors often maintain banking relationships that go structurally unexamined for years.",
    "Aureum was established to close that gapâ€”bringing institutional discipline to private wealth oversight."],
  fdr_personal:"Based in Luxembourg. American, Finnish, and Luxembourg citizen. Mother tongue Finnish.",
  board:"Advisory Board",
  acc_lab:"Global Access",acc_h:"From Helsinki to Singapore",
  price_lab:"Pricing",price_h:"One simple fee. Full transparency.",price_sub:"On average, clients reduce their total banking costs by 35%. Our fee: 0.15% annually for portfolios up to â‚¬2M. 0.10% for â‚¬2â€“15M. 0.05% for â‚¬15M+. Minimum â‚¬500/year. When we reduce your costs, we keep 10% of the savings. No commissions. No kickbacks.",
  /* v13: FAQ */
  faq_lab:"Questions",faq_h:"What clients ask us",
  faqs:[
    ["Do you provide investment advice?","No. We don't manage your money or tell you what to buy. We connect you with banks, reduce your costs, create clear reports, and benchmark your portfolio. You and your chosen bank make all investment decisions."],
    ["What does the Power of Attorney allow?","Read-only access to your portfolio reports. We can't trade, move money, or change anything. Your bank sends us reports. We turn them into clear summaries. That's it."],
    ["How much does Aureum cost?","We operate on a transparent hybrid model. First, an annual oversight fee: 0.15% for portfolios up to \u20AC2M, 0.10% for \u20AC2\u201315M, and 0.05% for \u20AC15M+. Minimum \u20AC500 per year. This covers coordination, reporting, and ongoing independent oversight. Second, when we achieve measurable reductions in your banking costs through structured reviews or negotiations, we participate in 10% of the documented, realised savings. This applies only to banking and structural cost reductions, assessed on a clear before-and-after basis. We never receive commissions, retrocessions, or inducements from banks."],
    ["What if I don't like any proposal?","Then you don't proceed. There is no obligation. You can keep your existing banking relationship, or ask us to search again with different parameters. We only earn a fee once you sign a PoA and we begin reporting."],
    ["Do I need to leave my current bank?","Not necessarily. Many clients use Aureum to benchmark their existing bank against alternatives. If your current setup is competitive, we\u2019ll tell you. If better options exist, you\u2019ll see them side by side. Some clients consolidate, others diversify across multiple banks."],
    ["How is my data protected?","All client data is GDPR-compliant and stored on encrypted EU servers. Your profile is anonymised before being sent to banks \u2014 they never see your identity until you authorise it. We provide a full data processing agreement before any engagement begins."],
    ["What is the minimum portfolio size?","EUR 250,000. At this level, we source proposals from Finnish banks. Above EUR 1M, Luxembourg and the UK become available. Above EUR 3M, Switzerland and the UAE open. Above EUR 5M, Monaco and Singapore."],
    ["Do you need a license to do this?","Aureum does not provide investment advice, manage portfolios, or execute transactions. We source banking relationships, produce reports, and benchmark performance \u2014 all informational activities that fall outside the MiFID II regulatory perimeter. This is a deliberate structural design."],
    ["How long does the process take?","Typically 2\u20133 weeks from onboarding to receiving proposals. We collect your profile in under 5 minutes, present it anonymously to competing banks, and coordinate meetings once proposals arrive. The entire process is managed by Aureum \u2014 you simply compare and decide."],
    ["Can you help with insurance wrappers?","Yes. We source proposals from insurance wrapper providers in Luxembourg, Ireland, and Finland alongside private bank proposals. Insurance wrappers can offer significant tax and succession planning advantages depending on your jurisdiction and structure."],
    ["What is Collective Strength?","We present your mandate alongside other Nordic investors when approaching banks. This collective reference AUM gives each individual client institutional-level negotiating power. Banks respond differently to â‚¬25M in combined volume than to â‚¬1Mâ€”better pricing, institutional share classes, priority service. Your data remains completely separate and confidential; only aggregated volume is communicated for negotiating leverage."],
    ["Why are my actual fees higher than what my bank quotes?","Most Nordic banks quote only the management fee \u2014 typically 0.50\u20130.70%. But your real cost includes multiple hidden layers. The largest is often FX spreads: every time your portfolio trades a non-EUR security, the bank embeds a currency margin of 0.30\u20131.00% that never appears on any statement. Add custody fees, underlying fund costs (especially with house funds), transaction costs, and platform charges, and your total effective cost often reaches 1.20\u20131.80%. International banks with all-in pricing and institutional share classes can deliver equivalent service at 0.60\u20130.80% total. We quantify every layer \u2014 including FX \u2014 so you see the real number."]],

  cta_h:"Access the world's best private bankers",cta_p:"5-minute conversation. Up to 15 proposals from top global banks. Bankers who speak your language. Lower costs. Clear reporting. No obligation.",cta_btn:"Start Now",
  ft_desc:"Access to 25+ global private banks. Bankers who speak Finnish, Swedish, or English. Lower total costs. Clear benchmarking. From â‚¬250K.",
  ft_cols:[["Service","What You Get","How It Works","Pricing"],["Company","About Noah","Jurisdictions"],["Contact","noah@aureumprivateoffice.com","Luxembourg City"]],
  ft_disc:"Aureum Private Office does not provide investment advice, manage portfolios, or distribute products. We source banking relationships, produce independent analysis, and benchmark performance. All outputs are informational. Aureum operates outside the MiFID II regulatory perimeter by structural design.",
  kyc:["Aureum Onboarding","Type your response...","End-to-end encrypted","Brief interruption â€” please try again."],
  we:["Starting portfolio","Time horizon","Return profile",["Conservative","Balanced","Growth"],"gross return assumed","years"],
  phases:["Welcome","Personal","Background","Financial","Requirements","Jurisdictions","Preferences","Complete"],
  pf:[["Personal",[["firstName","Name"],["nationality","Nationality"],["residence","Country of Residence"],["occupation","Occupation"]]],["Financial",[["totalInvestable","Investable Assets"],["currentBanks","Current Banks"]]],["Preferences",[["priorities","Priorities"],["jurisdictions","Jurisdictions"],["insuranceWrapper","Insurance Wrapper"],["bankerLanguage","Banker Language"],["reportLanguage","Report Language"],["email","Email"]]]],
},
fi:{
  nav:["Palvelut","Prosessi","Esikatselu","Tietoa","Hinnoittelu","Aloita"],
  hero_lab:"Maailman parhaat yksityispankkiirit. Omalla kielellÃ¤si.",
  hero_h:["Yhteys maailman johtaviin pankkeihin. ","Alhaisemmat kokonaiskulut. ","TÃ¤ysin lÃ¤pinÃ¤kyvÃ¤ kokonaisuus."],
  hero_p:"YhdistÃ¤mme sinut huippupankkiireihin yli 25 kansainvÃ¤lisessÃ¤ pankissa â€” pankkiireihin jotka puhuvat kieltÃ¤si. AlennÐ°Ð¼me kokonaiskulujasi, luomme selkeÃ¤Ã¤ raportointia ja vertailemme salkkuasi vertaisryhmÃ¤Ã¤n.",
  hero_cta:["Aloita haku","NÃ¤in se toimii"],
  hero_fq:"\u201CTuotot ovat hypoteeseja. Kulut ovat faktoja.\u201D",hero_fqa:"\u2014 Noah Kraama, Perustaja",
  stats:[["18+","Vuotta kokemusta"],["0%","Kickbackeja tai provisioita"],["25+","Pankkia kÃ¤ytettÃ¤vissÃ¤"],["Jopa 15","Tarjousta per haku"]],
  svc_lab:"MitÃ¤ tarjoamme",svc_h:"Globaali pÃ¤Ã¤sy. Alhaisemmat kulut. SelkeÃ¤ raportointi. Edistynyt analyysi.",
  svcs:[
    ["Yhteys huippupankkiireihin maailmanlaajuisesti","YhdistÃ¤mme sinut maailman johtaviin yksityispankkeihin â€” ZÃ¼richistÃ¤ Singaporeen. LÃ¶ydÃ¤mme pankkiirit jotka puhuvat kieltÃ¤si: suomeksi, ruotsiksi tai englanniksi. Tapaat heidÃ¤t. SinÃ¤ valitset.","Jopa 15 tarjousta"],
    ["Alenna kokonaiskulujasi","Tunnistamme jokaisen kulukerroksen jonka pankkisi veloittaa â€” mukaan lukien piilotetut kulut kuten valuuttamarginaalit ja rahastopalkkiot. Yhteisvoiman kautta alennÐ°Ð¼me kokonaiskulujasi keskimÃ¤Ã¤rin 0,50%.","Jatkuvat sÃ¤Ã¤stÃ¶t"],
    ["Vertaile salkkuasi","SelkeÃ¤t kuukausiraportit omalla kielellÃ¤si. Vertaisvertailut. Monte Carlo -simulaatiot. Stressitestaus. Edistynyt riskianalyysi. NÃ¤e miten salkkusi todella suoriutuu relevantteihin vertailuarvoihin nÃ¤hden.","Kuukausittainen raportointi"],
    ["Markkinatiedotus reaaliajassa","Kysy meiltÃ¤ markkinoista, sijoituksista tai trendeistÃ¤ â€” WhatsApp, Telegram tai Signal. Jaamme dataa ja markkinanÃ¤kemyksiÃ¤ salkkusi kontekstissa. Ei neuvontaa. Ei uutiskirjeitÃ¤. Vain relevantti tieto.","24/7 saatavuus"]],
  lang_lab:"Sinun kielesi",lang_h:"Keskustele varallisuudestasi suomeksi, ruotsiksi tai englanniksi",
  lang_p1:"Geneve, Luxemburg, Singapore â€” Ã¤idinkielellÃ¤si. LÃ¶ydÃ¤mme suomen- ja ruotsinkielisiÃ¤ pankkiireja kansainvÃ¤lisistÃ¤ pankeista.",
  lang_p2:"Raportit, WhatsApp-katsaukset ja kaikki viestintÃ¤ â€” valitsemallasi kielellÃ¤.",
  langs:[["Suomeksi","Suomenkieliset pankkiirit kansainvÃ¤lisissÃ¤ pankeissa","\"Valitsin suomalaisen yksityispankin, jossa on institutionaalista palvelua. Kun kaikki â€” raporteista tapaamisiin â€” on suomeksi, suhde omaan varallisuuteen muuttuu.\"","â€” T.L., YrittÃ¤jÃ¤, Helsinki"],["PÃ¥ svenska","Ruotsinkieliset yhteyshenkilÃ¶t verkostossamme","\"LÃ¶ysin ruotsinkielisen pankkiirin Luxemburgista, joka ymmÃ¤rtÃ¤Ã¤ pohjoismaista yritys kulttuuria. Vihdoin tulen ymmÃ¤rretyksi kunnolla.\"","â€” M.S., Family Office, Turku"],["Englanniksi","Koko kansainvÃ¤linen pankkiverkosto kÃ¤ytÃ¶ssÃ¤si","\"Aureum yhdisti minut pankkiiriin Singaporessa, joka hallitsee sekÃ¤ eurooppalaiset ettÃ¤ aasialaiset markkinat. Sujuvaa englanninkielistÃ¤ viestintÃ¤Ã¤.\"","â€” J.K., Tech-sijoittaja, Espoo"]],
  hw_lab:"NÃ¤in se toimii",hw_h:"EnsimmÃ¤isestÃ¤ keskustelusta jatkuvaan seurantaan",
  steps:[
    ["Jaa profiilisi","Ohjattu keskustelu kerÃ¤Ã¤ kaiken mitÃ¤ pankit tarvitsevat. Salkun koon perusteella tunnistamme sinulle sopivat alueet.","5 minuuttia"],
    ["Vastaanota jopa 15 tarjousta","LÃ¤hetÃ¤mme anonymisoidun profiilisi yli 25 pankkiverkostostamme valituille pankeille â€” priorisoiden niitÃ¤ joilla on sinun kieltÃ¤si puhuvia pankkiireja.","10 arkipÃ¤ivÃ¤Ã¤"],
    ["Allekirjoita valtakirja","MyÃ¶nnÃ¤t Aureumille valtakirjan jotta pankkisi lÃ¤hettÃ¤Ã¤ meille raportit. NeljÃ¤nnesmaksusi kerÃ¤tÃ¤Ã¤n automaattisesti.","Kerran"],
    ["Tapaa pankkiirit","JÃ¤rjestÃ¤mme tapaamiset sinun ja valittujen pankkiirien vÃ¤lille. SinÃ¤ vertailet, sinÃ¤ pÃ¤Ã¤tÃ¤t.","Omaan tahtiisi"]],
  sp_lab:"KÃ¤ytÃ¤nnÃ¶ssÃ¤",sp_h:"â‚¬2,3M salkku â€” 34 % pienemmÃ¤t kokonaiskulut",
  sp_intro:"Suomalainen teknologiayrittÃ¤jÃ¤. 8 vuotta samassa sveitsilÃ¤isessÃ¤ pankissa. Ei ollut koskaan vertaillut vaihtoehtoja. Kokonaiskulut: 1,45 %. Aureumin kautta: 12 tarjousta. Suomenkielinen pankkiiri lÃ¶ytyi. Uudet kokonaiskulut: 0,95 %. Se on 34 % vÃ¤hemmÃ¤n. Katso pitkÃ¤n aikavÃ¤lin vaikutus laskuristamme alla.",
  sp_steps:[
    ["PÃ¤ivÃ¤ 1","Jakoi profiilinsa Aureumin kanssa. Viiden minuutin perehdytys.","\u2713"],
    ["PÃ¤ivÃ¤ 3","Anonymisoitu profiili lÃ¤hetetty 15 pankkiin 4 lainkÃ¤yttÃ¶alueella.","\u2192"],
    ["PÃ¤ivÃ¤ 12","12 tarjousta vastaanotettu. Kolmessa pankissa suomenkielinen pankkiiri.","\u25C8"],
    ["PÃ¤ivÃ¤ 18","Tapasi neljÃ¤ pankkiiria videolla. Yksi tapaaminen GenevessÃ¤.","\u25A3"],
    ["PÃ¤ivÃ¤ 25","Valitsi uuden pankin. Kokonaiskulut laskivat 1,45 %:sta 0,95 %:iin.","\u2B25"]],
  sp_results:[["12","Tarjousta vastaanotettu"],["âˆ’34%","Kokonaiskulut"],["Suomi","Kielinen pankkiiri lÃ¶ytyi"],["â‚¬2,3M","Seurannassa"]],
  sp_note:"Nimet ja yksityiskohdat anonymisoitu. Aureum ei tarjoa sijoitusneuvontaa. Kaikki pÃ¤Ã¤tÃ¶kset olivat asiakkaan omia.",

  prev_lab:"Katso miten se toimii",prev_h:"TÃ¤ltÃ¤ raportointisi voisi nÃ¤yttÃ¤Ã¤",prev_tabs:["RÃ¤Ã¤tÃ¤lÃ¶idyt raportit","WhatsApp-katsaukset"],
  portal_lab:"Asiakasportaali",portal_h:"NÃ¤in nÃ¤et varallisuutesi. Aina ajan tasalla.",
  fdr_lab:"Perustaja",fdr_name:"Noah Kraama",fdr_title:"Perustaja \u00B7 Aureum Private Office",art_lab:"Perustajan kyn\u00E4st\u00E4",
  fdr_q:"Emme ole t\u00E4\u00E4ll\u00E4 korvaamassa pankkeja. Olemme t\u00E4\u00E4ll\u00E4 tuomassa kurinalaista vertailua.",
  fdr_quotes:[
    "Valvonta ei ole varallisuustason funktio. Se on vakavuuden funktio.",
    "Luottamuksen ja todentamisen tulisi kulkea rinnakkain. Vertailun ei pit\u00E4isi olla poikkeuksellista \u2014 sen pit\u00E4isi olla rutiinia.",
    "Yksityisvarallisuus ei tarvitse disruptiota. Se tarvitsee rakennetta."
  ],
  fdr_bio:[
    "Noah Kraaman vanhemmat ovat molemmat suomalaisia. HÃ¤n syntyi Yhdysvalloissa ja vietti lapsuutensa JyvÃ¤skylÃ¤ssÃ¤ ja HelsingissÃ¤, mutta on asunut suurimman osan elÃ¤mÃ¤stÃ¤Ã¤n Luxemburgissa. HÃ¤nen Ã¤idinkielensÃ¤ on suomi, ja hÃ¤n puhuu sujuvasti englantia, ranskaa ja luxemburgia sekÃ¤ jonkin verran saksaa ja espanjaa.",
    "IsÃ¤ rakensi lÃ¤hes kahden vuosikymmenen uran yhdessÃ¤ Sveitsin arvostetuimmista yksityispankeista, neuvoen monia Suomen varakkaimmista perheistÃ¤ Luxemburgista kÃ¤sin. Ã„iti rakensi uransa institutionaalisessa pÃ¤Ã¤omasijoittamisessa, jossa hallintokehykset ja mandaattikuri ovat perustavanlaatuisia.",
    "Kasvaminen tÃ¤ssÃ¤ risteyksessÃ¤ paljasti rakenteellisen kuilun. Institutionaaliset sijoittajat vertailevat systemaattisestiâ€”he neuvottelevat sÃ¤ilytyssopimukset uudelleen ja arvioivat rakenteita jatkuvasti. Yksityissijoittajat yllÃ¤pitÃ¤vÃ¤t pankkisuhteita, jotka jÃ¤Ã¤vÃ¤t tutkimatta vuosiksi.",
    "Aureum perustettiin kaventamaan tÃ¤tÃ¤ kuiluaâ€”tuomaan institutionaalista kurinalaisuutta yksityisvarallisuuden valvontaan."],
  fdr_personal:"Kotipaikka Luxemburg. Yhdysvaltain, Suomen ja Luxemburgin kansalainen. Ã„idinkieli suomi.",
  board:"Neuvonantajat",
  acc_lab:"Globaali ulottuvuus",acc_h:"HelsingistÃ¤ Singaporeen",
  price_lab:"Hinnoittelu",price_h:"TÃ¤ysin lÃ¤pinÃ¤kyvÃ¤ hinnoittelu. Ei piilotettuja kuluja.",price_sub:"KeskimÃ¤Ã¤rin asiakkaat alentavat kokonaispankkikulujaan 35%. Aureumin palkkio vaihtelee vÃ¤lillÃ¤ 0,05â€“0,15% salkun koosta riippuen. Kun alennÐ°Ð¼me pankkikulujasi, osallistumme toteutuneisiin sÃ¤Ã¤stÃ¶ihin. Ei palkkioita pankeilta. Ei kickbackeja. TÃ¤ysin riippumaton.",
  faq_lab:"KysymyksiÃ¤",faq_h:"MitÃ¤ asiakkaat kysyvÃ¤t",
  faqs:[
    ["Tarjoatteko sijoitusneuvontaa?","Ei. Aureum ei tarjoa sijoitusneuvontaa, hallinnoi salkkuja tai suosittele arvopapereita. Kilpailutamme pankkisuhteita, tuotamme riippumattomia raportteja ja vertailemme suorituskyky\u00E4. Kaikki tuotoksemme ovat informatiivisia. Sijoitusp\u00E4\u00E4t\u00F6kset pysyv\u00E4t t\u00E4ysin sinun ja valitsemasi pankin v\u00E4lill\u00E4."],
    ["Mit\u00E4 valtakirja sallii?","Valtakirja antaa Aureumille vain lukuoikeuden pankkiraportteihisi. Emme voi toteuttaa kauppoja, siirt\u00E4\u00E4 varoja tai tehd\u00E4 muutoksia tileihisi. Pankkisi l\u00E4hett\u00E4\u00E4 meille s\u00E4\u00E4nn\u00F6lliset salkkuraportit, jotka muunnamme selkeiksi yhteenvedoiksi."],
    ["Paljonko Aureum maksaa?","Toimimme lÃ¤pinÃ¤kyvÃ¤llÃ¤ mallilla. Vuotuinen valvontapalkkio: 0,15 % salkuille alle 2 Mâ‚¬, 0,10 % vÃ¤lillÃ¤ 2â€“15 Mâ‚¬ ja 0,05 % yli 15 Mâ‚¬. VÃ¤himmÃ¤ismaksu 500 â‚¬ vuodessa. TÃ¤mÃ¤ kattaa koordinoinnin, raportoinnin ja jatkuvan riippumattoman valvonnan. Kun saavutamme mitattavia sÃ¤Ã¤stÃ¶jÃ¤ pankkikuluissasi, osallistumme 10 %:lla dokumentoiduista sÃ¤Ã¤stÃ¶istÃ¤. TÃ¤mÃ¤ koskee vain pankki- ja rakennekulujen vÃ¤hennyksiÃ¤. Emme koskaan saa palkkioita tai hyÃ¶tyosuuksia pankeilta."],
    ["Ent\u00E4 jos en pid\u00E4 mist\u00E4\u00E4n tarjouksesta?","Silloin et etene. Ei velvoitteita. Voit pit\u00E4\u00E4 nykyisen pankkisuhteesi tai pyyt\u00E4\u00E4 meit\u00E4 hakemaan uudelleen eri parametreilla."],
    ["Pit\u00E4\u00E4k\u00F6 nykyisest\u00E4 pankista luopua?","Ei v\u00E4ltt\u00E4m\u00E4tt\u00E4. Monet asiakkaat k\u00E4ytt\u00E4v\u00E4t Aureumia vertaillakseen nykyist\u00E4 pankkiaan vaihtoehtoihin. Jos nykyinen j\u00E4rjestelysi on kilpailukykyinen, kerromme sen. Jos parempia vaihtoehtoja l\u00F6ytyy, n\u00E4et ne rinnakkain."],
    ["Miten tietoni on suojattu?","Kaikki tiedot ovat GDPR-yhteensopivia ja tallennettu salattuihin EU-palvelimiin. Profiilisi anonymisoidaan ennen pankeille l\u00E4hett\u00E4mist\u00E4. Toimitamme t\u00E4yden tietojek\u00E4sittelysopimuksen ennen toimeksiannon alkamista."],
    ["Mik\u00E4 on v\u00E4himm\u00E4issalkkukoko?","250 000 euroa. T\u00E4ll\u00E4 tasolla kilpailutamme suomalaisia pankkeja. Yli 1M\u20AC avaa Luxemburgin ja Britannian. Yli 3M\u20AC Sveitsin ja Arabiemiirikunnat. Yli 5M\u20AC Monacon ja Singaporen."],
    ["Tarvitsetteko toimilupaa?","Aureum ei tarjoa sijoitusneuvontaa eik\u00E4 toteuta transaktioita. Kilpailutamme pankkisuhteita, tuotamme raportteja ja vertailemme suorituskyky\u00E4 \u2014 kaikki informatiivista toimintaa MiFID II -s\u00E4\u00E4ntelyn ulkopuolella."],
    ["Kuinka kauan prosessi kest\u00E4\u00E4?","Tyypillisesti 2\u20133 viikkoa liittymisest\u00E4 tarjousten vastaanottamiseen. Ker\u00E4\u00E4mme profiilisi alle 5 minuutissa, esit\u00E4mme sen anonyymisti kilpaileville pankeille ja j\u00E4rjest\u00E4mme tapaamiset tarjousten saavuttua."],
    ["Voitteko auttaa vakuutuskuorien kanssa?","Kyll\u00E4. Kilpailutamme vakuutuskuoritarjouksia Luxemburgista, Irlannista ja Suomesta yhdess\u00E4 yksityispankkitarjousten kanssa. Vakuutuskuoret voivat tarjota merkitt\u00E4vi\u00E4 vero- ja perint\u00F6suunnitteluetuja."],
    ["Mik\u00E4 on Yhteisvoima?","Kun l\u00E4hestymme pankkeja, esit\u00E4mme mandaattisi yhdess\u00E4 muiden verkostomme pohjoismaisten sijoittajien kanssa. T\u00E4m\u00E4 antaa jokaiselle yksitt\u00E4iselle asiakkaalle merkitt\u00E4v\u00E4sti suuremman yhdistetyn varallisuuden neuvotteluvoiman. Pankit reagoivat eri tavalla 25M\u20AC:oon kuin 1M\u20AC:oon \u2014 parempi hinnoittelu, institutionaaliset rahasto-osuusluokat ja etuoikeutettu palvelu. Tietosi pysyv\u00E4t t\u00E4ysin erillisin\u00E4 ja luottamuksellisina."],
    ["Miksi todelliset kuluni ovat suuremmat kuin pankkini ilmoittaa?","Useimmat kotimaiset pankit ilmoittavat vain hallinnointipalkkion \u2014 tyypillisesti 0,50\u20130,70 %. Suurin piilotettu kulu on usein valuuttamarginaali: joka kerta kun salkkusi kauppaa ei-EUR-arvopaperia, pankki sis\u00E4llytt\u00E4\u00E4 0,30\u20131,00 % valuuttamarginaalin joka ei n\u00E4y miss\u00E4\u00E4n tiliotteella. Lis\u00E4\u00E4 s\u00E4ilytyspalkkiot, rahastojen sis\u00E4iset kulut, transaktiokulut ja alustapalkkiot, ja kokonaiskulusi nousee usein 1,20\u20131,80 %:iin. Kansainv\u00E4liset pankit kokonaishinnoittelulla tarjoavat vastaavan palvelun 0,60\u20130,80 %:lla. Me kvantifioimme jokaisen kerroksen \u2014 my\u00F6s valuuttakulut."]],

  cta_h:"PÃ¤Ã¤sy maailman parhaimpiin yksityispankkeihin",cta_p:"Viiden minuutin keskustelu. Jopa 15 tarjousta maailman johtavilta pankeilta. Tapaat pankkiirit jotka puhuvat suomea. SinÃ¤ pÃ¤Ã¤tÃ¤t. Yksi lÃ¤pinÃ¤kyvÃ¤ palkkio â€” ei piilotettuja kuluja, ei kickbackeja. Ei sitoutumisvelvoitetta.",cta_btn:"Aloita haku",
  ft_desc:"Riippumaton varallisuuskonsierge. Jopa 15 kilpailevaa tarjousta yli 25 pankilta, pankkiiriyhdistÃ¤minen suomeksi, ruotsiksi tai englanniksi. TÃ¤ysin riippumaton.",
  ft_cols:[["Palvelut","MitÃ¤ saat","NÃ¤in se toimii","Hinnoittelu"],["Yritys","Tietoa Noahista","LainkÃ¤yttÃ¶alueet"],["Yhteystiedot","noah@aureumprivateoffice.com","Luxembourg City"]],
  ft_disc:"Aureum Private Office ei ole toimiluvan alainen sijoituspalveluyritys eikÃ¤ tarjoa sijoitusneuvontaa. Kaikki raportointi on tiedoksi. Aiempi tuotto ei ennusta tulevia tuloksia.",
  kyc:["Aureum-liittyminen","Kirjoita vastauksesi...","PÃ¤Ã¤stÃ¤ pÃ¤Ã¤hÃ¤n salattu","Hetkellinen katko â€” yritÃ¤ uudelleen."],
  we:["Aloitussalkku","Aikahorisontti","Tuottoprofiili",["Maltillinen","Tasapainoinen","Kasvu"],"oletettu bruttotuotto","vuotta"],
  phases:["Tervetuloa","HenkilÃ¶tiedot","Tausta","Taloustiedot","Toiveet","Alueet","Asetukset","Valmis"],
  pf:[["HenkilÃ¶tiedot",[["firstName","Nimi"],["nationality","Kansalaisuus"],["residence","Asuinmaa"],["occupation","Ammatti"]]],["Taloustiedot",[["totalInvestable","Sijoitettava varallisuus"],["currentBanks","Nykyiset pankit"]]],["Asetukset",[["priorities","Prioriteetit"],["jurisdictions","Alueet"],["insuranceWrapper","Vakuutuskuori"],["bankerLanguage","Pankkiirin kieli"],["reportLanguage","Raporttikieli"],["email","SÃ¤hkÃ¶posti"]]]],
},
sv:{
  nav:["TjÃ¤nster","Process","FÃ¶rhandsvisning","Om oss","PrissÃ¤ttning","Kom igÃ¥ng"],
  hero_lab:"Din oberoende fÃ¶rmÃ¶genhetskoncierg",
  hero_h:["BÃ¤ttre villkor. ","BÃ¤ttre rapportering."," BÃ¤ttre informerad."],
  hero_p:"Vi tar fram upp till 15 konkurrerande fÃ¶rslag frÃ¥n Ã¶ver 25 av Europas ledande privatbanker â€” och matchar dig med en bankir som talar ditt sprÃ¥k. Oberoende rapportering, personliga mÃ¶ten och lÃ¶pande uppfÃ¶ljning. Helt oberoende och avgiftsbaserad.",
  hero_cta:["Starta processen","Utforska tjÃ¤nster"],
  hero_fq:"\u201CAvkastning \u00E4r hypotes. Kostnader \u00E4r fakta.\u201D",hero_fqa:"\u2014 Noah Kraama, Grundare",
  stats:[["18+","Ã…rs bankarv"],["0%","Kick-backs eller provisioner"],["25+","Banker tillgÃ¤ngliga"],["Upp till 15","FÃ¶rslag per sÃ¶kning"]],
  svc_lab:"Vad du fÃ¥r",svc_h:"Fyra tjÃ¤nster. En avgift. Inga Ã¶verraskningar.",
  svcs:[
    ["KonkurrensutsÃ¤ttning","Upp till 15 fÃ¶rslag frÃ¥n Ã¶ver 25 banker i 7 lÃ¤nder. Genom vÃ¥rt Collective Strength-program presenteras ditt mandat tillsammans med andra nordiska investerare â€” vilket ger dig institutionell fÃ¶rhandlingskraft. Vi matchar dig med en bankir som talar ditt sprÃ¥k.","Vid start + pÃ¥ begÃ¤ran"],
    ["SkrÃ¤ddarsydd rapportering","Med fullmakt skickar din bank oss portfÃ¶ljrapporter. Vi omvandlar dem till tydliga, visuella sammanfattningar.","MÃ¥nadsvis eller kvartalsvis"],
    ["ResultatjÃ¤mfÃ¶relse","Vi jÃ¤mfÃ¶r din fÃ¶rvaltares resultat oberoende mot liknande mandat och marknadsindex.","PÃ¥ begÃ¤ran + kvartalsvis"],
    ["WhatsApp-insikter","FrÃ¥ga oss om marknader eller din portfÃ¶lj. Vi delar marknadsdata och uppskattningar baserade pÃ¥ din senaste rapport.","24/7 via WhatsApp"]],
  lang_lab:"Ditt spr\u00E5k",lang_h:"Internationell bankverksamhet. P\u00E5 finska.",
  lang_p1:"Vi identifierar finsk- och svensktalande bankirer p\u00E5 internationella banker s\u00E5 att du aldrig f\u00F6rlorar m\u00F6jligheten att diskutera din f\u00F6rm\u00F6genhet p\u00E5 ditt eget spr\u00E5k.",
  lang_p2:"Rapporter, WhatsApp-insikter och all kommunikation \u2014 p\u00E5 det spr\u00E5k du v\u00E4ljer.",
  langs:[["Suomeksi","Finsktalande bankirer pÃ¥ internationella banker","\"Having a banker in Geneva who speaks Finnish changed everything.\"","â€” M.K., Tech Founder, Helsinki"],["PÃ¥ svenska","Svensktalande relationsansvariga i vÃ¥rt nÃ¤tverk","\"Att kunna diskutera min fÃ¶rmÃ¶genhet pÃ¥ svenska med en bankir i Luxemburg Ã¤r ovÃ¤rderligt.\"","â€” J.L., Family Office, Vaasa"],["In English","TillgÃ¥ng till hela det internationella banknÃ¤tverket","\"Aureum found me a banker in Singapore who understood Nordic and Asian markets.\"","â€” A.R., Portfolio Manager, London"]],
  hw_lab:"SÃ¥ fungerar det",hw_h:"FrÃ¥n fÃ¶rsta samtalet till lÃ¶pande uppfÃ¶ljning",
  steps:[
    ["Dela din profil","Ett guitat samtal samlar allt banker behÃ¶ver. Baserat pÃ¥ din portfÃ¶ljstorlek identifierar vi vilka jurisdiktioner som finns tillgÃ¤ngliga.","5 minuter"],
    ["FÃ¥ upp till 15 fÃ¶rslag","Vi skickar din anonymiserade profil till banker utvalda frÃ¥n vÃ¥rt nÃ¤tverk av 25+ banker â€” med prioritet fÃ¶r de som har bankirer som talar ditt sprÃ¥k.","10 arbetsdagar"],
    ["TrÃ¤ffa bankirerna","Vi schemalÃ¤gger e-mÃ¶ten eller personliga mÃ¶ten. Du jÃ¤mfÃ¶r, du beslutar.","I din takt"],
    ["Skriv under fullmakt","Du ger Aureum en fullmakt sÃ¥ att din bank skickar oss rapporter. Din kvartalsavgift dras automatiskt.","LÃ¶pande"]],
  sp_lab:"I praktiken",sp_h:"FrÃ¥n en bank till tolv fÃ¶rslag",
  sp_intro:"En finsk teknikentreprenÃ¶r baserad i Luxemburg hade haft sin fÃ¶rmÃ¶genhet hos samma schweiziska bank i Ã¥tta Ã¥r. Han hade aldrig jÃ¤mfÃ¶rt villkor, aldrig trÃ¤ffat en annan bankir, och hade ingen aning om hans avgifter var konkurrenskraftiga. Hans kontaktperson talade bara engelska och tyska.",
  sp_steps:[
    ["Dag 1","Delade sin profil med Aureum. Fem minuters introduktion.","\u2713"],
    ["Dag 3","Anonymiserad profil skickad till 15 banker i 4 jurisdiktioner.","\u2192"],
    ["Dag 12","12 fÃ¶rslag mottagna. Tre banker hade finsktalande bankirer.","\u25C8"],
    ["Dag 18","TrÃ¤ffade fyra bankirer via video. Ett personligt mÃ¶te i GenÃ¨ve.","\u25A3"],
    ["Dag 25","Valde en ny bank. Totala kostnader sjÃ¶nk frÃ¥n 1,45% till 0,95%.","\u2B25"]],
  sp_results:[["12","FÃ¶rslag mottagna"],["0,50%","Avgiftsminskning"],["Finska","Talande bankir hittad"],["â‚¬2,3M","Under bevakning"]],
  sp_note:"Namn och detaljer anonymiserade. Aureum ger inte investeringsrÃ¥dgivning. Alla beslut fattades av kunden.",

  prev_lab:"Se det i aktion",prev_h:"SÃ¥ hÃ¤r kan din rapportering se ut",prev_tabs:["SkrÃ¤ddarsydd rapport","WhatsApp-insikter"],
  portal_lab:"Kundportal",portal_h:"SÃ¥ ser du din fÃ¶rmÃ¶genhet. Alltid aktuell.",
  fdr_lab:"Grundaren",fdr_name:"Noah Kraama",fdr_title:"Grundare \u00B7 Aureum Private Office",art_lab:"Fr\u00E5n grundarens penna",
  fdr_q:"Vi \u00E4r inte h\u00E4r f\u00F6r att ers\u00E4tta banker. Vi \u00E4r h\u00E4r f\u00F6r att inf\u00F6ra disciplinerad j\u00E4mf\u00F6relse.",
  fdr_quotes:[
    "Tillsyn \u00E4r inte en funktion av f\u00F6rm\u00F6genhetsniv\u00E5. Det \u00E4r en funktion av seriositet.",
    "F\u00F6rtroende och verifiering b\u00F6r samexistera. J\u00E4mf\u00F6relse b\u00F6r inte vara exceptionellt \u2014 det b\u00F6r vara rutin.",
    "Privat f\u00F6rm\u00F6genhet beh\u00F6ver inte disruption. Den beh\u00F6ver struktur."
  ],
  fdr_bio:[
    "Noah Kraamas fÃ¶rÃ¤ldrar Ã¤r bÃ¥da finlÃ¤ndare. Han fÃ¶ddes i USA och tillbringade sin barndom i JyvÃ¤skylÃ¤ och Helsingfors, men har bott stÃ¶rre delen av sitt liv i Luxemburg. Hans modersmÃ¥l Ã¤r finska, och han talar flytande engelska, franska och luxemburgiska samt lite tyska och spanska.",
    "Hans far tillbringade nÃ¤rmare tvÃ¥ decennier vid en av Schweiz mest etablerade privatbanker och rÃ¥dgav nÃ¥gra av Finlands fÃ¶rmÃ¶gnaste familjer frÃ¥n Luxemburg. Hans mor byggde sin karriÃ¤r inom institutionell private equity, dÃ¤r styrningsramverk och mandatdisciplin Ã¤r grundlÃ¤ggande.",
    "Att vÃ¤xa upp i denna korsning avslÃ¶jade en strukturell klyfta. Institutionella investerare benchmarkar systematisktâ€”de omfÃ¶rhandlar depÃ¥avtal och omvÃ¤rderar strukturer kontinuerligt. Privata investerare behÃ¥ller bankrelationer som fÃ¶rblir ogranskade i Ã¥ratal.",
    "Aureum grundades fÃ¶r att Ã¶verbrygga den klyftanâ€”att tillfÃ¶ra institutionell disciplin till privat fÃ¶rmÃ¶genhetsÃ¶vervakning."],
  fdr_personal:"Baserad i Luxemburg. Amerikansk, finsk och luxemburgsk medborgare. ModersmÃ¥l finska.",
  board:"RÃ¥dgivande styrelse",
  acc_lab:"TillgÃ¥ng",acc_h:"Ã…tta jurisdiktioner. En process.",
  price_lab:"PrissÃ¤ttning",price_h:"Se vad lÃ¤gre avgifter gÃ¶r Ã¶ver tid",price_sub:"Genom Collective Strength presenteras ditt mandat tillsammans med andra nordiska investerare. Vi identifierar dolda avgiftslager som lokala banker sÃ¤llan avslÃ¶jar. NÃ¤r vi minskar dina kostnader deltar vi i bara 10 % av de dokumenterade besparingarna. VÃ¥ra intressen Ã¤r helt i linje med dina.",
  faq_lab:"FrÃ¥gor",faq_h:"Vad kunder frÃ¥gar oss",
  faqs:[
    ["Ger ni investeringsr\u00E5d?","Nej. Aureum ger inte investeringsr\u00E5dgivning, f\u00F6rvaltar inte portf\u00F6ljer eller rekommenderar v\u00E4rdepapper. Vi f\u00F6rmedlar bankrelationer, producerar oberoende rapporter och benchmarkar resultat. Alla v\u00E5ra utdata \u00E4r informativa. Investeringsbeslut f\u00F6rblir helt mellan dig och din valda bank."],
    ["Vad till\u00E5ter fullmakten?","Fullmakten ger Aureum enbart l\u00E4s\u00E5tkomst till dina bankrapporter. Vi kan inte utf\u00F6ra aff\u00E4rer, flytta tillg\u00E5ngar eller g\u00F6ra n\u00E5gra \u00E4ndringar p\u00E5 dina konton. Din bank skickar oss periodiska portf\u00F6ljrapporter som vi omvandlar till tydliga sammanfattningar."],
    ["Vad kostar Aureum?","Vi arbetar med en transparent hybridmodell. F\u00F6rst en \u00E5rlig tillsynsavgift: 0,15 % f\u00F6r portf\u00F6ljer upp till \u20AC2M, 0,10 % f\u00F6r \u20AC2\u201315M och 0,05 % f\u00F6r \u20AC15M+. Minimiavgift \u20AC500 per \u00E5r. Detta t\u00E4cker koordinering, rapportering och l\u00F6pande oberoende tillsyn. N\u00E4r vi uppn\u00E5r m\u00E4tbara besparingar i dina bankkostnader deltar vi med 10 % av de dokumenterade, realiserade besparingarna. Detta g\u00E4ller endast bank- och strukturkostnader. Vi tar aldrig emot provisioner eller kick-backs fr\u00E5n banker."],
    ["Vad h\u00E4nder om jag inte gillar n\u00E5got f\u00F6rslag?","D\u00E5 g\u00E5r du inte vidare. Ingen f\u00F6rpliktelse. Du kan beh\u00E5lla din befintliga bankrelation eller be oss s\u00F6ka igen med andra parametrar."],
    ["M\u00E5ste jag l\u00E4mna min nuvarande bank?","Inte n\u00F6dv\u00E4ndigtvis. M\u00E5nga kunder anv\u00E4nder Aureum f\u00F6r att benchmarka sin befintliga bank mot alternativ. Om din nuvarande uppst\u00E4llning \u00E4r konkurrenskraftig ber\u00E4ttar vi det. Om b\u00E4ttre alternativ finns ser du dem sida vid sida."],
    ["Hur skyddas mina uppgifter?","All data \u00E4r GDPR-kompatibel och lagrad p\u00E5 krypterade EU-servrar. Din profil anonymiseras innan den skickas till banker. Vi tillhandah\u00E5ller ett fullst\u00E4ndigt personuppgiftsbitr\u00E4desavtal innan n\u00E5got uppdrag p\u00E5b\u00F6rjas."],
    ["Vad \u00E4r minsta portf\u00F6ljstorlek?","250 000 euro. P\u00E5 denna niv\u00E5 s\u00F6ker vi f\u00F6rslag fr\u00E5n finska banker. \u00D6ver 1M\u20AC \u00F6ppnas Luxemburg och Storbritannien. \u00D6ver 3M\u20AC Schweiz och F\u00F6renade Arabemiraten. \u00D6ver 5M\u20AC Monaco och Singapore."],
    ["Beh\u00F6ver ni licens f\u00F6r detta?","Aureum ger inte investeringsr\u00E5dgivning eller utf\u00F6r transaktioner. Vi f\u00F6rmedlar bankrelationer, producerar rapporter och benchmarkar resultat \u2014 all informativ verksamhet utanf\u00F6r MiFID II."],
    ["Hur l\u00E5ng tid tar processen?","Vanligtvis 2\u20133 veckor fr\u00E5n introduktion till f\u00F6rslag. Vi samlar din profil p\u00E5 under 5 minuter, presenterar den anonymt f\u00F6r konkurrerande banker och koordinerar m\u00F6ten n\u00E4r f\u00F6rslagen anl\u00E4nder."],
    ["Kan ni hj\u00E4lpa med f\u00F6rs\u00E4kringsomslag?","Ja. Vi s\u00F6ker f\u00F6rslag fr\u00E5n f\u00F6rs\u00E4kringsomlagsleverant\u00F6rer i Luxemburg, Irland och Finland vid sidan av privatbankf\u00F6rslag. F\u00F6rs\u00E4kringsomslag kan erbjuda betydande skatte- och successions planerings f\u00F6rdelar."],
    ["Vad \u00E4r Collective Strength?","N\u00E4r vi kontaktar banker presenterar vi ditt mandat tillsammans med andra nordiska investerare i v\u00E5rt n\u00E4tverk. Detta ger varje enskild kund f\u00F6rhandlingskraften av betydligt st\u00F6rre sammanlagd f\u00F6rm\u00F6genhet. Banker reagerar annorlunda p\u00E5 25M\u20AC \u00E4n p\u00E5 1M\u20AC \u2014 b\u00E4ttre priss\u00E4ttning, institutionella andelsklasser och prioriterad service. Din data f\u00F6rblir helt separat och konfidentiell."],
    ["Varf\u00F6r \u00E4r mina faktiska avgifter h\u00F6gre \u00E4n vad min bank anger?","De flesta nordiska banker anger bara f\u00F6rvaltningsavgiften \u2014 typiskt 0,50\u20130,70 %. Den st\u00F6rsta dolda kostnaden \u00E4r ofta valutamarginaler: varje g\u00E5ng din portf\u00F6lj handlar ett icke-EUR-v\u00E4rdepapper till\u00E4mpar banken en dold marginal p\u00E5 0,30\u20131,00 % som aldrig syns p\u00E5 n\u00E5got utdrag. L\u00E4gg till dep\u00E5f\u00F6rvaringsavgifter, fondkostnader, transaktionskostnader och plattformsavgifter, och din totala effektiva kostnad n\u00E5r ofta 1,20\u20131,80 %. Internationella banker med totalpriss\u00E4ttning erbjuder ofta motsvarande service till 0,60\u20130,80 % totalt. Vi kvantifierar varje lager \u2014 inklusive valutakostnader."]],

  cta_h:"Redo att se vad som finns?",cta_p:"Fem minuter att dela din profil. Upp till 15 fÃ¶rslag frÃ¥n Ã¶ver 25 banker. MÃ¶ten med bankirerna. Du beslutar. Inga dolda avgifter, inga provisioner â€” en transparent avgift. Ingen fÃ¶rpliktelse.",cta_btn:"BÃ¶rja din sÃ¶kning",
  ft_desc:"Din oberoende fÃ¶rmÃ¶genhetskoncierg. Upp till 15 konkurrerande fÃ¶rslag frÃ¥n Ã¶ver 25 banker, bankirmatchning pÃ¥ finska, svenska eller engelska. Helt oberoende.",
  ft_cols:[["TjÃ¤nster","Vad du fÃ¥r","SÃ¥ fungerar det","PrissÃ¤ttning"],["FÃ¶retag","Om Noah","Jurisdiktioner"],["Kontakt","noah@aureumprivateoffice.com","Luxembourg City"]],
  ft_disc:"Aureum Private Office Ã¤r inte ett licensierat vÃ¤rdepappersfÃ¶retag och ger inte investeringsrÃ¥d. All rapportering Ã¤r informativ. Tidigare avkastning fÃ¶rutsÃ¤ger inte framtida resultat.",
  kyc:["Aureum-introduktion","Skriv ditt svar...","Krypterad frÃ¥n Ã¤nda till Ã¤nda","Kort avbrott â€” fÃ¶rsÃ¶k igen."],
  we:["StartportfÃ¶lj","Tidshorisont","Avkastningsprofil",["Konservativ","Balanserad","TillvÃ¤xt"],"antagen bruttoavkastning","Ã¥r"],
  phases:["VÃ¤lkommen","Personligt","Bakgrund","Finansiellt","Behov","Jurisdiktioner","Preferenser","Klar"],
  pf:[["Personligt",[["firstName","Namn"],["nationality","Nationalitet"],["residence","BosÃ¤ttningsland"],["occupation","Yrke"]]],["Finansiellt",[["totalInvestable","Investerbar fÃ¶rmÃ¶genhet"],["currentBanks","Nuvarande banker"]]],["Preferenser",[["priorities","Prioriteringar"],["jurisdictions","Jurisdiktioner"],["insuranceWrapper","FÃ¶rsÃ¤kringsomslag"],["bankerLanguage","Bankirens sprÃ¥k"],["reportLanguage","RapportsprÃ¥k"],["email","E-post"]]]],
},
};

/* â•â•â• AI SYSTEM PROMPT â•â•â• */
/* mkSys removed in v22 â€” structured KYC replaces AI chatbot */

/* â•â•â• DATA â•â•â• */

const JURIS=[{f:"\u{1F1E8}\u{1F1ED}",n:"Switzerland"},{f:"\u{1F1F1}\u{1F1FA}",n:"Luxembourg"},{f:"\u{1F1EB}\u{1F1EE}",n:"Finland"},{f:"\u{1F1EC}\u{1F1E7}",n:"United Kingdom"},{f:"\u{1F1F8}\u{1F1EC}",n:"Singapore"},{f:"\u{1F1E6}\u{1F1EA}",n:"UAE"},{f:"\u{1F1F2}\u{1F1E8}",n:"Monaco"}];
const BANKS_NORDIC=[
  {n:"Nordea Private Banking",loc:"Helsinki",min:"\u20AC250K",lang:"FI/SV/EN",spec:"Largest Nordic bank. Strong structured products, multi-currency accounts, and Nordic equity research."},
  {n:"OP Private",loc:"Helsinki",min:"\u20AC250K",lang:"FI/SV/EN",spec:"Cooperative bank with client-first ethos. Competitive custody fees, strong fixed-income offering."},
  {n:"Mandatum Private Wealth",loc:"Helsinki",min:"\u20AC500K",lang:"FI/SV/EN",spec:"Part of Sampo Group. Institutional heritage in asset management, strong insurance wrapper solutions."},
  {n:"Evli",loc:"Helsinki",min:"\u20AC500K",lang:"FI/EN",spec:"Boutique investment firm. Specialist in Nordic equities, alternative investments, and discretionary mandates."},
  {n:"Aktia Private Banking",loc:"Helsinki",min:"\u20AC250K",lang:"FI/SV/EN",spec:"Swedish-Finnish heritage. Strong bilingual service, sustainable investing focus."},
  {n:"\u00C5landsbanken",loc:"Mariehamn",min:"\u20AC250K",lang:"SV/FI/EN",spec:"Swedish-language specialist. Conservative, relationship-driven, strong in balanced mandates."},
  {n:"Danske Bank Private",loc:"Helsinki",min:"\u20AC250K",lang:"FI/EN",spec:"Part of the largest Danish banking group. Nordic expertise, strong digital platform, and structured lending."},
  {n:"SEB Private Banking",loc:"Helsinki",min:"\u20AC500K",lang:"FI/SV/EN",spec:"Leading Swedish bank with deep Nordic roots. Institutional-grade research, strong corporate-wealth bridge."},
  {n:"CapMan Wealth",loc:"Helsinki",min:"\u20AC500K",lang:"FI/EN",spec:"Private equity heritage. Unique access to Nordic alternative investments and co-investment opportunities."},
];
const BANKS_INTL=[
  {n:"Lombard Odier",loc:"Geneva",min:"\u20AC1M",lang:"FR/EN/DE",spec:"Oldest private bank in Geneva (est. 1796). Leaders in sustainability-integrated wealth management."},
  {n:"Julius B\u00E4r",loc:"Zurich",min:"\u20AC1M",lang:"DE/EN/FR",spec:"Pure-play wealth manager. Global presence, strong Asian markets desk, comprehensive advisory."},
  {n:"Pictet",loc:"Geneva",min:"\u20AC1M",lang:"FR/EN/DE",spec:"Partnership structure ensures long-term thinking. Thematic investing pioneers, institutional-grade research."},
  {n:"Bank J. Safra Sarasin",loc:"Basel",min:"\u20AC1M",lang:"EN/DE/FR",spec:"Swiss-Brazilian heritage. Strong sustainability focus, emerging markets expertise, family-owned stability."},
  {n:"UBS Global Wealth",loc:"Zurich",min:"\u20AC2M",lang:"20+ languages",spec:"World\u2019s largest wealth manager. Unmatched global network, lending solutions, and market access."},
  {n:"EFG International",loc:"Zurich",min:"\u20AC1M",lang:"EN/DE/FR/IT",spec:"Entrepreneurial culture. Each banker operates as independent practice \u2014 highly personal service."},
  {n:"Edmond de Rothschild",loc:"Geneva",min:"\u20AC1M",lang:"FR/EN/DE",spec:"Family-owned conviction-driven manager. Expertise in private equity, real assets, and estate planning."},
  {n:"VP Bank",loc:"Vaduz",min:"\u20AC500K",lang:"DE/EN",spec:"Liechtenstein heritage. Competitive fees, strong intermediary services, and digital banking platform."},
  {n:"LGT",loc:"Vaduz",min:"\u20AC2M",lang:"DE/EN/FR",spec:"Owned by the Princely Family. Ultra-long-term investment horizon, strong alternatives allocation."},
  {n:"Rothschild & Co",loc:"London",min:"\u20AC5M",lang:"EN/FR/DE",spec:"Two centuries of family wealth expertise. Bespoke advisory, generational planning, and M&A integration."},
  {n:"Berenberg",loc:"Hamburg",min:"\u20AC1M",lang:"DE/EN",spec:"Germany\u2019s oldest bank (est. 1590). Exceptional European equity research, personal relationship model."},
  {n:"BNP Paribas Wealth",loc:"Paris",min:"\u20AC1M",lang:"FR/EN/NL",spec:"Global scale with European roots. Strong credit solutions, insurance wrappers, and succession planning."},
  {n:"Soci\u00E9t\u00E9 G\u00E9n\u00E9rale PB",loc:"Paris",min:"\u20AC1M",lang:"FR/EN",spec:"Structured products leader. Innovative derivatives-based solutions for capital protection."},
  {n:"HSBC Private Banking",loc:"London",min:"\u20AC2M",lang:"EN/FR/ZH",spec:"Unmatched Asia-Europe corridor. Ideal for clients with cross-border business interests."},
  {n:"J.P. Morgan PB",loc:"London",min:"\u20AC5M",lang:"EN/FR/DE",spec:"Institutional-grade investment platform. Access to alternatives, co-investments, and global deal flow."},
  {n:"Deutsche Bank Wealth",loc:"Frankfurt",min:"\u20AC2M",lang:"DE/EN",spec:"Strong corporate-wealth integration. Excellent for entrepreneur-clients with business banking needs."},
  {n:"Vontobel",loc:"Zurich",min:"\u20AC1M",lang:"DE/EN/FR",spec:"Swiss quality with digital innovation. Strong thematic investments, structured products, and active management."},
  {n:"Citi Private Bank",loc:"London",min:"\u20AC5M",lang:"EN/ES/ZH",spec:"True global reach across 100+ countries. Capital markets access, art advisory, and aviation finance."},
  {n:"Union Bancaire Priv\u00E9e (UBP)",loc:"Geneva",min:"\u20AC1M",lang:"FR/EN/DE",spec:"Independent Swiss private bank. Strong conviction-based investing, hedge fund expertise, and family governance."},
  {n:"Quintet Private Bank",loc:"Luxembourg",min:"\u20AC1M",lang:"EN/FR/DE/NL",spec:"European multi-country network. Headquartered in Luxembourg with offices across 50 European cities."},
];

/* â•â•â• v16: QUARTERLY REPORT DATA â•â•â• */
const MC_DATA=Array.from({length:21},(_,i)=>{const y=i;const base=2312;const g=1.06;
  const m=base*Math.pow(g,y);return{y,p5:Math.round(base*Math.pow(1.01,y)),p25:Math.round(base*Math.pow(1.035,y)),p50:Math.round(m),p75:Math.round(base*Math.pow(1.085,y)),p95:Math.round(base*Math.pow(1.11,y))}});
const STRESS=[
  {sc:"2008 Financial Crisis",eq:-38,fi:-4,re:-25,tot:-22,rec:"18 months"},
  {sc:"2020 COVID Crash",eq:-34,fi:+2,re:-18,tot:-16,rec:"6 months"},
  {sc:"2022 Rate Shock",eq:-18,fi:-12,re:-8,tot:-14,rec:"12 months"},
  {sc:"Eurozone Sovereign Crisis",eq:-22,fi:-6,re:-10,tot:-14,rec:"14 months"},
];
const BENCH_BEFORE=[{m:"Jan",p:100,b:100},{m:"Feb",p:102,b:101},{m:"Mar",p:98,b:96},{m:"Apr",p:101,b:99},{m:"May",p:104,b:102},{m:"Jun",p:107,b:105},{m:"Jul",p:109,b:107},{m:"Aug",p:106,b:103},{m:"Sep",p:108,b:105},{m:"Oct",p:112,b:109},{m:"Nov",p:115,b:112},{m:"Dec",p:116,b:113}];
const BENCH_AFTER=[{m:"Jan",p:100,b:100},{m:"Feb",p:102,b:105},{m:"Mar",p:98,b:101},{m:"Apr",p:101,b:108},{m:"May",p:104,b:111},{m:"Jun",p:107,b:115},{m:"Jul",p:109,b:119},{m:"Aug",p:106,b:116},{m:"Sep",p:108,b:120},{m:"Oct",p:112,b:124},{m:"Nov",p:115,b:127},{m:"Dec",p:116,b:133}];

const FOUNDER_IMG="data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCAIVAZADASIAAhEBAxEB/8QAHAAAAQUBAQEAAAAAAAAAAAAABgIDBAUHAAEI/8QAUxAAAgEDAgIGBQYJCAgGAgMBAQIDAAQRBSESMQYTQVFhcSIygZGxBxQjcqHBFSQzQlJistHwNGNzgpKiwuEWJTVDU3Sj8SZEVIOTszZkhMPSF//EABoBAAMBAQEBAAAAAAAAAAAAAAABAgMEBQb/xAAsEQACAgICAQQCAgEEAwAAAAAAAQIRAzESIUEEIjJRE3FCYfCBkaGxBSPB/9oADAMBAAIRAxEAPwADjbht38B91XNzYBwvzgGGThUB2J4dwMDJ3U+B27qpCp+YuR2oeXlW1dRYavZQwXMfFIkKLk+i4HCOR7R7xWGRtaN4tLZjtxb3FrJwzxkjHPvH3+dLhuDwcJHWx8wpO48jRvqfRG6so3a0xdWmc9XwnK+ajcea+4UJT6UJG6y1JSQnPVsRv5Hk3xpRy/ZTgpaPYbnALBzLGOe3pp5jtFFHRnpnf6DIvzaUXFkx4mt3OUPip/NPlt4UDNxwzYlDRSryblg0oN1TllPVSE5LKPQY+K9nmPdWyZi4UaPquqW2p6DdvDJ6bSKzROfTH0aqT4jIO9BswYyJggDDZ+zFM2t8sriKUCOY8lzkOO9T2/GlXs3VyKuGOUYnA5bUMg0L5L8f6Sn/AJdz9q1sEwzC4zj0Tv7KyD5LhnpKSOXzZ/ita/N+Qk+qfhVrwDI9uMT8uw/GmNf/ANh3Wf0R8RT9uPxg+R+NM68A2iXQPLh+8VUvkRDQJdBo1kvrl8AOLOFQwG4G5+6jB1wxVhuvaKFOgf8ALbv/AJaD4Gi6b8q3sxQthLREhJF2+eXCv30B9OGHzrUicbQ/4qOs/jEpB7F++gHpwfxrVc/8AH7TSlscTMoz9Mp71Ufaa135PtfS20dLS5QLD1rBZR2HmQffWQIfpU8APvrWOiegPddEIry0bNwZZCyNjDjOMfZ2+8VCKLnpsVc2rhgVPIjlyan+iCH/AEY0k99uD9poPv5LiAMhLgRElrWUn0diCVPZz/eO2jLoZLDN0W03qZVkMMAjkCndW7j3GqTEwN6dkm91I4Awijn+s9ZwgBubg+X3Vo/Tr+U6ljGwX38clZxGcXE+e0gfZUyGhxvyLfWH30thuvmKQ2Opb6w+Bp1uY8xUDG5dgPrD41Y2KF8KB6RdgP7RquuD6Axz4h8autGA+c2+3OX/ABVUQN0FivUqHt0JVQDjt2pv8HRn/csPbVrXVRNGadOIQk1nwg8O3/2CjSWwDOxE3aditDvSqMSanoqHcGVM+P0g/dRwVB5gGhxQyhbSgTnMTeJWgjpjEIZmXGw6v3+lWn3CILeRgoBCnGKzfp2Ar8R7TH/j/dS412IBJh+MQN3yj7FNHfQQutvfujAHrEHqcXY1AkzEPAR/xSD/AGTWnfJrbMNMv5cj05lGCO5f86VWMtzwyH6S3s5PrxAGoesQW/4HuGWzjjdQCrxyEAHIHLtopa3z2KfZVJrcavpV2AAAIWbl3EUcWFg/0b06wubG6muoZXf53KoZN+XDVv8AgzTg2EurmEdxUr9oxXnRG0DaJMZI2Ia9nZSDjbix91XhsowM/SqPOk0wBfU4Ra9V1N4Z0d+BlY5IHCTnc+FAMa8V3Z8zm5X760zW4QsceDnEpwT9U1m1qpN7p4B53A+BpUNEm4yNSm/5pvg1DeqHKWv1m+Aolu/9p3H/ADcnwahrU+Vr5t8BUjehheVKI2NJHKldhqBEY0kmuJpJNZHQjjzrzixSS1Nk71LGP9ZtSfns8AIifh4uZprOaRJyFRRVleFJspANgqbeIxW43ejzRW0EhUsvVIyunMeiN/8AtWO2MKTei26uqgge419Lvp7wwKsADRBQBGwzsBj+CPtr0HG0ctgBHfTW5HXZkQcpEG48wOfmKZv9HsNajMnBHHI5z18X5/1hyJ8efjRReaPBdMxj+hm/RPafv+w0OXVjcafOWUmJydzjKP5jv9xrFwKUgM1nRLnT0Burc3FuD+WQ5Cjz5jybPnQvcWRjy0D8cY5qQcr5j7+XlWux6ih+jmXqnIwAd1byP3GqDVejFtcnr7Bltpxv1e/Bnwxuvs28KSuJqpJ7MwlVZozE4yM5Hge8Hv8AEVNVLqBGjM7TR8JUCTmcjke//KrPUrIQOy6hAqzYJBQgFh44237CPsqDNeJJaxSNEFnK8IK+qcZGSO/YVtGVmU0HHQrWYuj2qrcyIZIyhjbffBxv9lbTa6laarp7T2kyyIV3xzXwI7K+Z4Jmt2+lIQHYMD6DH28j4Vfafr17pcwe0uXhkAwSv3g7GrTM2fQEa8NwccsH41G1440W58h+0KGuifTuHV8W2ohLe7AwHBwkv7j4cqI+kAzodyBvsP2hV3bElSB3oOvBeXa//rW/wNFcp+mcbchQt0JH47e7cre3H92ilhmeT2fCmtky0QEH4xKPBPvoE6cpi41IkHHU8/a1HsAzcy+SfA0BdOxl9T546nf3vSlsImXRn6dfIffW8/JyR/odbgEEiSTOOz0qwQA/OFxz2++ty+ThHi6HxM23HPKy+WcfdURLbI/ygRwJNDOV+lEbAnvHC+PhQ9pIudMis7i2c210bdDxMPQlUjYOM4wew5x4qavflCfiNspHpFCfsernQ9OttU6I6XFOucWq8Dj1kJUZwfiOR7c06AzzpXqBvhdSSQm3lZU6yJzvxAuSVPaPSHiO2gRN7mcD9IfCjjpVDNbQz28jBlhYBTjs4nUfs8uzOOVA0TYu7jzHwqWBIP5Fs/pL8DS3PLzpon6FvF1+Bpb7keYqRnSbhfrD41d6Llru1A3zKP2qopNgv1h8aIejozqViOX0y/t1Udgb8OQr2urqoQFdIRnpBoin/ip/9lGtBWvNnpLoQPIyxk/2mo1psBq53tpPqms2+UM8LD60Q+xzWlXBxbvnurMvlJb6RQOfHFn+y9HgXkAnfMsA/nSf7hrXfk530Kc/z5/ZFY6pzcR+Dn9g1svydDHR6Q9pnP7K1KGF1UGqn/VN8P5l/wBqr+h/WFzpdyOzq/8AGKuImOdExjQU/ppf2zVxP/J5Pqn4VU9Ff9gQ/wBJL+21W828En1TS8jKHWlAtRsCRL/hasusD/rLSx+lcD4GtS13C2KE8zIf/rest0wcWraOvfcA/wB01EwQ9df7SuP+bm+DUOar61oPrfAURXJ/H7g//s3B+xqHNVP0lr5N91Zsp6GRypR9U+VJHIV6fUbyqBEPi2pJrzNdWTNrEmmyaWabY0ijga8fkK8zXHeoZSJlkCb4cQwSU+019QD1RXy1pUzS36cRyeJRnyNfUq+qPKvRWjlY1PaxXAPGoz31U3tg6RnrFEsOOZ5j+PH31eV1FCM61bRoRA8kbAx4y0bbmhq0haGaZRNJw8YGCScDA7aNruMCwkGxHD2f1qG44gLqXK7ZGceVRONDjIAulgxrDKf/AEwPvJoZb+T2viHH2minpnE0eucR9V7VcHyJz8RQsfyFpn9b76mBtLSLuNGfKhC68J4hjO3bkd1e9S0e8BBX/hk7f1T2fDyq36MK7awvBEZSIpCVCFtsb7Df3ZPgavbzo/baiOtsGEMzgkJzV+/BGx9mCO0VdmIJW91wMSpIZeanYjzH8Ci6x6d3tvp7WNwPnMDDA4mwy+R/fQnfWMtrII7qJo5B6jjt8j93vFQi0kWCzDh/SC7e3u8+XlTsDcOg11b3s9/PbuWTq4V3GCCFxgj2UVsPpX9nwr5+0XXrnSbpZrWcxS47Dsw+8Vpmg/KRp9/OLbU1WznbAEufomPifzfbt41akS10FUA/G5PJPgaz/px6Tatnl1IHh60taJHhbiRxup4cN2cv86znpnlYtZb9XH96WmxRMwX+UgeAPxre/k9XPQu0Ujbif9o1gibXqDvA++t9+T//APDbPzf9o1CKKX5RD1cluQf92wHueiHomcdGNK8bZPhQ/wDKKgc2+5DDJxjn6L0QdGkA6N6SoOwt05+QqhMznpq3E18364H/AFJazxf5ROf1x8K0Lpmo6u+I/wCIv7b/AL6z1BmWbffrPuqGND5/It9cfA0ps4HnXn+5b64+Br1+zzqSkdKR6Az+evxoh6NZ/Cmnj+fX9qhuQ5Mf11+NXuh3Jtry0n2ykituMjY1SBn0NXUIp0tucZaK2PtZfiKeXpflTxWkZOPzbgffVEkLXdulGhpnH0kfLzc/dRrWb6jrPzrpDpV3LaPEkUqgBZFctjiPZ5/ZRivSOyPrR3KD9aE/dTbAs7gAwOD3Vl/yjjhnPeZ4z/0zR7N0h0wQMWnZR4xN+6s46d6jZ6jKHtZ+sHXKfUZdgmM7jvpeAAobXER/WP7NbP8AJ4P/AA45752+C1iyIPnocE5OQRnbYd3tra/k+GOjA/pm+ApIbCqqPU8LpN0f5vHveryqTVyBo8+dwQq7eLirWiWe9FBjo5b57WkP/Uareb8g/wBU1WdGV4ej1qAc+sf7xqzm3hfypeRlJ0iwNPTfHpOR/wDG9ZZpAzr+i+M2PsFad0pPDaIM8opj/cP76zXRh/4h0QdnX/4RUyBDcpzcynvnuD9hof1T8va/Vb7qvnOZHPfJcn7KoNV/lFt9RviKxZXgaHKvW9RvKvByr1vUbyqREGu7K6uIrJmyEGmm5061NNSZQ2TilLuKbY0uP1TUsaHNI/lkRH/EGf7VfVQ9UeVfKukENew4/TUe3NfVQ9UeVegtHPI9rq6upkglOudOk+qP8VD8URS9JZWCsykZGxHL4iiWRQdOfu4V/wAVVxVGkgVSG4Y14sHkcsceynkRMTOvlGto49Qt3XI4rdsju9Qj40BDi6mywo348/bWkfKMnDqVuNvStnIHdgJWeRgmG08n++sVs6H8UHPQgyR9IkeIqHEMhHEMjkNq0Ca3s9RlYuptbxubAZWQ+I5N57MO+gn5Po0bpGrSLxRi2l488gMAVol3pWQxgPWLzKNzH8fwaJJ7MbKG/wBPYxNDqVuJoW2EgOc92Cefk2G7iaEdS6LzW6tPYEzwg4Kn1lPdvvnwO/ia0CO6mtyY3BkTGGR+eO7fmPOkNZRTZm0+TgkAwYmOMeAJ5DwbK92OdSpVsZjsluRkJ6BU+lGwwM+X5p/jFNJKwZldSDndTucd/j7K0jU9Hs9RZ1uIza3aDdwOHHdxDfA969xoM1bRLrTiVuouKLmJV5efh58vGtLsC26OdNL/AEBRAG+eacwwbeRt0B/QP5vly8quNf1Oz1nSNUu7OTiRlT0GGGQ5k2I8jz5VnfA8TFvWB5sB6Q8++lxzdobhzsCDswPMU7FQkb6hGOz/ACNb98n/AP8Ah1n5v+0awJFlbUshOKNRkkHPDz5jsz9xrfugAx0NsvN/2jTQFX083nhyMgRMR/Ykog0BSnR/TQd8QRj7BVB07H00R7DE2/8AVer/AEaRU0LSlx68MWMeQqhGa9OFCxXuCCOtT9pv31nMTfTTjucfCtF6Z7212cY+mj+P+dZ3GMSzk9smKiRUR/P0Df0g+Br2Ts86bORbtk/7wfA04/Z5/vqSvIh/Xi/pF+NX/R3q/wAJ6d1oBTrU4gRnIzVEwy8X9ItEnReBZtY01GGVMybe2qjsTN4ZYTkMinw4RTE1lYyowe1hYkY3QVKMSsc9tNtBgZVyMd9X0R2BOs6ZZf6UaXapbokLyx9Yo2B9Fz9womPRvTSPRjdT+rIRQ3q4abpzpSLsVniYnHcjmjRklOSOH30AVcnRy3CHq7m5Q/XzWcdOrV7OVYWlMoWXAYjGfQB++taYyJjiXIPbmsu+Uls3oHL8Y/8A6lpNAgDjP4wM9nH91aV0SsNTuNF6+3HodawAExQ9nsrNoxifP1vurZvk+nDdFxnbhndfPkfvpIpjhs9fi2R5yPC4DfEVWXZ1dbeWOe5v1iYrnrYkYD0hjBx30cmUY7PfVTrjqNLznZpYlA/riqomwf0LW76HR4FEQ4BxcJaFiD6R7RU+TpJdmJh1Vpns42dR8KseikqP0W05k9UxfeatJIYpRho0bv4lBpDsBdV1m8vbRmktbPCRSLxR3ROzLjOOGhPRiB0l0XwlJPuFH3S6C3gtGMUKJIYJWJUY7APvrPdEUv0o0dc/nP8ABahghsndvO4P2UP6rn51bD9RviKvx6pPeLg/CqDVf5Xb93Vt8RWbK8CF5V63qN5GvF5V635NvI1IiEBSuHauUU6F2rBs6EiO4xUd6mSLtUWSlYEdqXAMhvOkvTlv6redD0NHmi/ymE98iftV9WjkK+UdH2ubcjl1qj+8K+rhyFehHRhPZ7XV1dTIBlv9muMZ9Ef4qprdHgu5ZpInCZGDjGdsYHefCrsj8QbyH+KqQ2wupruKQcXGoT0t+zIqpkxA75RG49Thk4TwNbPwEqQeUecg+ORWdw46uz58m++tG6fx9VeQxk+rbuMZzjaI/fWcxnC2IPc/31itnR/FGqfJWoPSGY7bWrftLWozaap9K3bqm58P5v8Al7PtrLfko36QTd4tm/aWthrTwYg7d2yO3V3URVzsrDt8jyP2HwqpuNPlgIliJdRydOY/j+BRtJGkqFJFDIdirDINV0+mvHl7Zs/zbn4E/A+8VLimAKtPDcxrHepxcPqSplWQ94I3U+W3fUSewlghPVgXdqRkrw7gfVHxT2rV9cWMNyzBgYZwMnIx7x9+48arJILnT3zyXOc/mn91ZtNDAjUOi0NzmbSnCORn5ux2P1SPu9woUuLJ45XjljaGXtVhsfMcj51rU7Wl71nHG0U4IZmAzk9hPf57Ed4oV1mUyie1uYlZ4gSHbc+YO3eNzv5007CgCaR7SYvIW2IyA3rDGNv860Tol03m0iFYc/OLInPVnYr347vKs31dOsWIej6ToMty3NKt5m04rEyvwb+lniPP7RVBVm1dIda07XrRJrG46x0jk6yIjDp6Dbkd3iNqKdJjJ0PSGGAVijyD3FRWAx3YZVljlK52Vkb4H7q0vor0/tzb2+m6wBbmLgWK6TZCBgAOPzdts8j4VViKvpsMW11g/wDmIxv5Cs6AHFKf50/CtD6Ztx2cj5BD3KnI3BHCuCKzyNgGlzy60/ClIaFnBhOeXWD4Utzy8/303zgP9KPhTjjl5/vqSjm9aLv4xRX0OAPSHTB/PLQkxxJEcE4fOBzOxow6Gr/4k00fzq1S2KRudJk/Jt5GlUmT8m3kaokC7k56dWQPZMoH/wAJ/fRtQTcjHT6y8Zv/AOk0bU2A3MMqPrCsn+Uk41BQP+OT/wBNK1p+Q8xWSfKQP9ZIf59//rjpeA8gREOK4372+Irbugkar0WhwBgyOeXjWIW5JuD5t8RW6dCRjotbeLP+0aSGy+MaYPoL7qoddONJYncCWLH9qiA8jQ90hITSgT2zRjHvqlpk+SR0Yt0TotpajIAt1Ox7xn76s2Ux8mJ37arejchPRTSn2GbaP4VYOcOAfChCYOdMP5PIf/0ZfitZ90fA/wBLdHXxc/s0f9MfRtJzjb5jIM/1loE6PqD0v0odwc/CokWiCm8Wf5uc/CqLVf5ZAMf7s/Gr2IZtwf5mb4rVFqv8vhH80f2qyY3oQvIV6/5NvI14OVev+SfyNSxIjxjNSVTamYhmrCGLK8q5ZujriiBKm1QZRvVvPFgcqq5hgmpUgkiG4p21GUbzpDinrQfRv9aqb6JWyHpDkXtqO6VB9tfWg5CvknSgPwhbd/Xr8RX1sOVejHRhPZ7SGkRSQW3GNvOl02yqz54/AjsNUQURH4k/kP8AFVbZgfhGbzX4VZ4/EnHl/iqusRnU5+/K/CqkTEC/lJ9LVlBxgQOPshrLEYYsPqv99ar8pQC6mO0/N5Gx3bQ1kwO1iO5X++sFtnR/FGs/JP8A/kU//Kt+0tbHWLfJVMU6TOuMhrV87b7FTW0KcqDgjPYa18GJ7XV1dQA1PbRXKgSoDg5U8ip8D2VR3UTQyyQhuJe8jv8A450Q1TXozdz+Q+AoqxMEkixM4x+j8KFtaJOp6if0FK/3VozCAzPt+j8KEtfj4NS1QYxt/hWsqplWZ1rH8lX2ffT0GmG4tIpAxjkfIQuMK4BxseXvxTOrjNqBy3X760Poz82m6I2ttf2qzW/WSFWHNfSPtHs9tE266Li0tmcGGeynZWVopORBHot5j+DU62vA5CseBjyQnIP1T9xo01Pouwg47QG+ssbRn8rEPA9o8sjw7aCrzSGjVngJliHrIR6S+Y+/l41Cn9mjgpaLBryX5ibYOxgDhhGfzW8O7lVTF6ZkJBB6xjuKaW7khADlnXOAQfTXyJ5+Rp6JuJHkyW4nO5GNsCtLMqocH5E93W/dTjnYef76b2+bg/zv3Ut9gvn++kB6SBJCe59/caMOhX/5Lpg7esHwNBsjY6s/rZ+w0ZdChnpNpZ5Eup/u1URM3KkS/km8qXSX3Q1ZIGTZ/wD+h2oPLrWx/wDDRrQbcLj5RbLfmXP/AEaMqbATIMgedZH8op4tSQY266X9lBWuPyHnWQdPyTqkY7OumP2qPupPQAVa/wApPm37Vbv0LGOill4hv2jWFWu8zeBP7Vbx0PGOilh9Rv2jSQF2fVNDfSj/AGSv9Kp59ysaJG9Q+VDPSvbS4/Fj/wDW1UtCZL6OEnoppBO5+aRE/wBkVaMwYqPbyqDocQj6O6XHxbraRDvz6IqWpBmGO04NMl7Bvps2LGfHMWb/AGutBHR7P+mOneEch+FG/Tlf9X3JxztCP760D9Hs/wCmdljkLaQn31nI0RXx/wAlU/8A68h/vLVFq3+0Iv6L/EavYt7Nf+Wf9taotU/2kg/mR+0ayY2JHKvJTiF/I16KTPtbyfVNSxLYm23xV9Zwcajah+wbiYCjLSoONV2515/qJcTvwrkVN9blVORQ/cLhjRvqtrwodqD7xMOajDOyskaKpudSLP8AJN9b7qZkG9SbNfoW+t91bt9GC2Velfy+L+mT4ivrcchXyPppxew8t5l+Ir64HKvThowybOqPNGRKJFwTttnBr2WVkbIIK4wR3eNR3lBYBjvjfNWkYSktEFh+LS8+z/FVZYjGpz+a/CreVD83lxvn97VV2K41KfIxkr8KchxAr5TF/wBboM87SQn3xCsl6q4huIYbiBoniypDc+Wd+41q3ylSf67YZzw2si7dn5Db7aAdYjc6veTjeKeQyo43VlbcEH+O2sI7Z0S6ig8+SlUPSdyxPELV+Ee1c1tFYx8lEir0mlBO7Wr49hWtnByMitVoxOrq6m3RieJXK9476AHKqLsZu5vq/cKmrOxIXhwzEjPdUGfAnfGMcPZ7KpIlvopETN04+r8KE+liCPVNR/WiB/urRepEVw7vwgKASM+HhQp0sbjvdRfGxhyPcKzaGjKtW4jCOXDldu3Oa13oZpkU/QuxFwjxSs0rRyAesOM48/t8qyHVSTbbd6/GvojoGsU3QLTI5FVlMbZVt/z2pVZb0DN1Y3emkyxnMfPjTdT5iqq7s49ZjZnj6m5Vtp4zg57z30b6vagRXCITwg4AJz30PwwcC8OObj41nKFDjIxq/l4pni4RxI5BbABJHlTlsfxSMeJH2Cmb5SLmVjnd35+Yp+D+SReZ+6iOjTIO5zbY/nT8KXIcqh7z++k/+WH9I37Nc/qp5/caozG7qPrVjXMmCSCEODyPu86ItE1lbG5iuraR0lhI5xMOE4xjBFULHEkGAD6fI+RqUNPkjIMepXy8jvIrD7VpoRoy/KPqg/OhYd5jp1vlLvurwI7TiG5yp/fWc9VcjJGoTeTJG33CvOrus/ymJj3vbg/A1XYqQdRdNZZdft9TuIIGaHi9GMkZyvD2k0Ux/KNat61lIPJ/8qyFI7hsF/mr+cTD7zTnAwORDb8XbwyMv3UWwo12b5RdORAfmlwxzyBX99AnSjV7bWruKe3iljAaQkSY/OIPYT3VQHrW24SBnsmPKmnEiMx45wTjPpqw9xosKI+n3ccmpyWp4xIMn1dvWPbW7dE9RsU6N2ULXcKyIpDKzgEHJ76+etTUwPa3iPMJ4HLjCFuLcZBxyGB2VZ6f0gup1Ly26wxEDgHE2e3vG3tougo+jzcwPGxSaJtjycUN9LyZNNi6shgBKx4TkfkmrIW1scJAZDnsMoHxptryNvycbMP1Cv76OQUb1oi40DTdjn5rEM4/UFTgMkfur58i1e6g2jm1CIAD1GYD7DU+36WaohwNY1FezDlzj3g0+QuJo/Twn8H3AXGRbD/7FoL6P7dMoD3Wj/4qhS9J7u9R4rnVTKjrwMJAOWc4zgdte9HruGXppG0UqOq2MgPA+Rk57vZUt2NIbi/kS/8AKn9sVQap/tVR/Mj4miCMfiS/8r//AGCh7U99VA7oV+JrNjZwpFyfxWXH6NOAbU3cj8Vl+rUCWyJYycFwoPfWm9HYeNFPlWUglXBHMVrXQeVbzTVkByV9E+Feb69VCzv9LKm7JOt2eIiQKzjUk4ZWrYdXtg1u23ZWU6zFw3D1x+jyW6N8tSgpA1IN6mWI+gb633VHlAyal2A/Fyf1j8BXpS0cq2UFlmO/jVlZT167EEdtfXWRw5PLFfHryuOvBdiFJIy2a+slldY42yd0BJ5jcdtepjVo5crqh24jh4chipblgZFMPl3yXDjGOLhPfyrmnWP0MDh37ab+j4TIr7IMqMYJ7/vrVI5rtnhz81kB5j97VCtVBvpm7OJT9lSkwbKXhzjJx5ZaoNiD8/m3IHEvLyqZGkQA+UwEa6xHL5sxPvgFZVHM7RWScR4CjMVztnB3x7a075TImOvXHBIUxHxsMesB1GR/HdWVRAgWDZP5A1gts6ZfBGpfJa3F0txj/wApL/hrcEPEgNYZ8lR/8ZY7PmkvxWtujciRVJ25VutHM3UqHiwUZJAHjSWkVe2ulQyJwhuE5znGaivacTY60YABOQKEl5Bt+D2QRSSEruwGfS9Woku9xLn+OVP4kBcLhjj9Lh9ophhl3OWPifZVLZL0VkcQN24I2IHwoR6YRLDPqCg7C3H7vuozh3vm2Ixw/ChHp0As+pkdtsCfeazZSMf1Q+gBnmy7e2voXoBAW6B6SVc54ZDk74y7V87aucRDvyvxr6F+Ti5Zugenl91USjI7MSsAKUS3on6h6lzn9IcvNqpRGDwsF4yWHCoIBY52Az21d3YLQ3JO/p9vm1VkMayW7NwCQxuWVSdieW/sJp5F0KOzCtej6m+nXGAJHx7lNN23pW8ZDZAzt7ql9LUCXk4QYUOwHh6KVWabkQsv5oxw+0VjHRvkJ3/lgP51v2RXr8kHj91eN/JV/pG/ZFet+Z9b7qozObJlgCnfiP7Jq901ZJr62jjK8cjoi8QyN9tx2iqMfymEeLH+6aI+jiFukGmKDg/OI8HyINNCYXNoTcmisGPaSpH3UkdH0POysm+q+KPgZZPSEi8OfzkB86ZKSEAlLRs8uJME/ZT4snkgEPR5c7aWhHhMP30k9HYzudMmH1JRRyEVmw9nbbdo4sD7KeGnh0DCwXB7UlxScZD5Jmet0ctwMm1vVPdz+6h7VrWC2kiEAkHEW4lk55Bx++tentIYGRZLeVGfIU9ZkZAzWWdKFKaig/XkP9+krvsAY1K4S14pHiMqiOQ8AbGTnvqEIevfro1h4JVBAeZQw8696RScNmSASSjjb21pHQfS5rrodZSJbxupeXGXUH1yORod10aRpdszg6fcOpxHC4O2BMp++mPwS/Fg6exPei5+FbU3R6RvW0tW9itTR6Mw5y2jD/4F+4VnciuUDHPwc8Qx81vIyT2Fh99KZZ0yonvoyO9mrXj0dsw3EdLZWHaEdfhTR6Naec4hukzz4Z5R9hNLnLyh3BmVW95qCne6dkI5kA/EUV9E76WfUpFdgxFs7+qBjnXdKrOLTmS2t2lxNGXfjfiOOLAH8fdTfRFCNSuc8xZv2dm9VGVoU10TV/kmP/1l/wDtoc1Mf63P9En30Rr/ACX/APjR/wD2mhzUd9Zf+iT76GZPR6OVIuR+KS/VpxRtSLr0bSX6uKkSKc0a/JrrKWWu/g+4fhivBwoT2Sdg9vL3UFmm3Z0UsjFWG6kbHNYZcSywcH5NYycXZ9HatLawW/4zcQw5G3WyBc+81kuvPbSXDmC5hkB7UcEUOJi44ZmGS4By2599O8OOVcuD/wAdHD3ys2Wd8eJFnjdSTjI7xvUuw/k2f1z91MO2D3U/ZH8Wz3ua3yx4roIO2CoTjaUfpnHvr60S0DoqB3yoAyRtsB76+S45RFKHI9WQE++vrv53EsYJPYK9HFddHNmrqyN82dVkUONtgsiZBHgef/aopUjDqsT42PVsR28/ZjvqbNdRl48xktvjntUKZgCzMETY5Vk59/L2e+tuzB0LTeylOTuc789y1QrAfj8/1l+FTYgfwe+QQccickbtUSx/l9xjnlPhUSLRnXykj/Xtzlsn5s+B3D6GsiRj/q/P/p8/ZWsfKKT/AKRX2cDED4Oc7ZhrKOH09OA/9N91YR2zpl8Eaf8AJUVHTHJzn5pL8VrZluADhRvnmd8VjnyVRM3StnA9S0kz7SgrYRb5L+i+eQK4511Y6rs4p8uXRLjuFcjxOAO3lSbow9WS6gnsBqLGXiULwMGA5EUriaRusyEPLJOcezxoaV9DUrVM8KEyAhSwbkcgAeFNhSruGUKd9gNuyvQOJQF4SSxJIzzrxTl27fHPgtMRFhH48fIfCgzp9tLqn/LD4t+6jWH+Xt5D4UG9Phl9WO4xbLz83rNloxfVV44QO3iX419BfJ5b8Pyf6YWK8P0rkczvKx7K+ftQy3CFGW4lwO85rfvk4ljb5PtKOSX4ZeIIfUPWNz8d6mOy3oub3e2uWAHrZH96q+xhxfysR9CCOJcZ3GMVYXQPzGbffiA327TUfTWVfnMjZCqQwx5VUiYmEdKRxzy4HOQ/sLVfaRdVAuN8gDJ8AKtul8bRXMo7pmHuVf3VXwAmzhbvJ+6sI6OjIesD82UH/iP8BXrjHB5/dSm/k0f9K/wFeSc18/uqjM4fymLyb9k0U9FRx9KtNVcEiZSM+AoW3FzGcbYb9k0UdDgzdLdMxz60dmeynElmy8QWMcOTgbDwNeF0bhB2I9EHOR7KbaYP6LJ1Yc7A+G37qfULOMLxKD6PEh2BI3OfIdvfXQ+jLYtFbqS4QsGOcFRv41ItrlAgDuOLmT2Ypp2aJhmMkAYQc+I9rH2VHWSSRMAMMekcjmfupbQaZI1LhkNuQQRxMR/ZNY90ywuqxAdjS/tmtbYgvGgJZhksT5Gsk6cDg1qNQc+lKf8AqGs5I0TAPpA/4oR/Nt99bX8nC4+T/S2dUKnrSRw/zjH7qxPXhm0I742++tv+Twf+ANJ2Ynq32zyPG29EFbDI6ggrMAaFpFt0O+RlQMjwpKRJ1fGIxgkAMORz91Lc8Ft1Snk2TkbkZ/j3VMjYqkiswdk32xnHZVNIhOyCUkjZAVG+2FdufvrmDEeizgqVyeMkHffnXF3nXC7Mo4hueX/avIiSW4cblSRj3Gk4oFLszHp3akR21xj0urZT5ca//wCqq+iShtQvn7rJx9jUTfKAgXTIhjJ6on/qJQz0PDfPtQIJ4PmM+3kvP7TWCVdHS3cUScfip/5eL/7DQ3qH+2n/AKNPhRMR+LH+gh/bahq/H+upfqJ8KTM3oUKbux+Jyez4inlFIux+KP7PjUMSKbhrmhYrspPsqXG0a7kZqQdR6uMrGijPbiobZqkvJF00g2qrgsyErj2/9qItR6M6xpumDULmzjFrgFpI5gxjycDiHtHfzobtLhUnnRiAWIkHjkYPwpd1qs8kBtY7iQ2xILJxHhYg5G3gacm/AKhid96lWb4tR5mqxnzzqTby4gA86xkrLi6B9kUuxHaAf71fWUuRhOqJ4R62Cfh4V8lyZWedRz4TjwxmvrNMyxLsWIjUtx8h6P316GFmPqFo4uGA4WHW4yvEuPcT8KQYMq5uGKsDtlQQfb/H2Uua4mUH6MlMeqMEY2+zxqOZmdH4QSgODldxjx+6tmc/RKVAlpKg5L6I9haodgv+sLk+K/s1OjBNi2QQcDIPfk5qJYD8euPNf2azkaIyzp/k9IdQBHNZBv2+lBWXojcemkjb5pv/AGa1f5RyPw9ckHJET8vrw1lx2l09BsPmmf7grFbZ1P4I075LVYdK2KEDhtJCc+a4rZY5S7Z3GSQQR3VjHyZtjpeANibSX4rWxBghAYlsnIcfm1vHRyN0yTKuYyOENULGSVJYgHB37qkG7TcAHw8ajvKrysxjySMLg4/g1STJlJPyNSyLgKByGMg74ryEeiWyd85z7KWSgjZCpYNscjmNuzvrosEPhSBy357BaqwRGtx+PP8A1fhQP06BxrW52iX4vR3b730mRjHDv37UD9PFwNZ8YU+L1mykY/ccEdxFJIxWMSJxHGcDPOtt+TSzez6DxqzcSTXUrpwekpXIGduXqnnWH6ttCcfpIPtre/k7Df6A6YOBmHFMSB2jrHqYbLlov5gDBN2jrOzzNM2SkJIVIGd8sMj21KcZhl/pM/aaasweqfGNiedOQkYR0xJkuZ27fnDn7BVZAD8xh82+6rDpeCl7Mh2HWMedQbfBsYPbWEdG+Q7hJgi2261/gK9lX1P47KVt83hHaZnx7lpTDJXPf91UZjQH08QP6L/CivocCOlmmkdko+FC7pieI9vA/wAKK+hy8XS/Thy9MnPsNVET0a0wMjgH1G9IjPL7NqXbREcKGVlQ8jtz8v30hVk42BAAGMN37U5HxNL1bsPSBRcnkfLtrpejnvssJerWHDNsBzPZUCfNwd8BcAbZxzzuO3bl50pLN+HiLcY7ME7+X7zUd36o81w24zjI9tQkU2yUgHWQkKBz2HZ7ax7ppk6vCzc+GTP/AMrVscPE0sfFgEjl3bVjnTN1bVoMDCmNzju+lapkXHQDa4cWv9Tn7TW5dB44z0G0hkZ1+iJwTn85t/476wrXTm0I7erH7Rrdug8a/wChejcTeiId14ezib/OljfYZe4oIy5VcnhYhjtxY7u6pUF1EIgoThxkHsxTDwIqIF4mHCSXBxy8P45UwGOQC7cJHEQVOQN81o+zJXEskwqO3AY8DAyahxABgVPdkA06/DsoIMTAYG+x8O6m4VYFGbPLG/maiy9sA/lEIfTkZHyohA2/pR+6hjoguJtWbG6Wc+PAFB2+w0VfKGFGmhe3q0/+3/KhzokoEOuNnlZv+waxezo/iOMMW7/0UA/vNQzfb61P4Kn7IoocfQP9SD/FQvef7auf6g/uipZDHAKbvjiyfzHxp5RTGo/yJvrL8agSKjir0DLAHtpNLj9YVLNBq7jVbjYDblTRGKk3e8pPgKjHlSAZdsUpJSFApDV4tICunzxSy42JYV9YKJDDHwH1oUBydgMDevlS7X8QPZl3++vquKFHtLdiXyI0I3B/NHf++uvB0T6jtI8K3HDwjGSeHZgNx502803BwkAjJGFxjPsqXxP1YTCr6WdvvqJPB1it6rcRzjOwPnW92c2idEMaeR28O/vNRbEfj1wPFf2alwgCxI22HZ5mo9kMXlznvX4VnI2iZT8oamLXr3iYElHcY7AWi/dWaEfjVj/yf+EVqPylb65dYHK3J/6kdZeTm5s9sfiY/ZFc62zpl8EaX8miZ6WEkgcNpKd/Na1xWOGDY25YJ+NZH8m2T0uXB3+ay/4a1rjPAVbA8Tvjvrrx6ODKuxoTABjwscbHHZSldC5xksN9+zalqA6EdbwOrH0sjHupog8Q4WDEnJONv45VpZPEdS1aThZpF57jnXQJwLIgPFwkjIXHd2UwWljBOSGUkbHlUm2PWRkgYA2AznlioZcdDNuM3sn9X4UC9OjxprBxt1aj3GSj23H47L/V+FAnTYERayf1F+MlQy4mO6oMQk42DJ8a375OyV6Aac3XYCmYnGP+I229YHqxHUkd5T9qt3+T1H/0FsDgqrCUZ/8AdbfNTDZctBGfStmPewP2mohmeC3UohbMmCeQHbv5napjHNu573+81Dkm6nTnwQC7cG6lu8nb2U5iiYh0yybudiCfxiQb1WW4/EoPI/GrXpkSLyQnGTPNkeNVsCn5hAfBvjWEdHRlFqv4rEe3rX+6vWGyef3UpP5LF/SSf4aURkJ5/dVGQgr+NQ5H5jH7KKehQLdLLE8sFjufA0MSnFxBjf0W+Aoq6FBj0sscHGQ37Jqo7Jlo1R0BWR+Ph4cEqdyc9lJVUjfGZDISSUJAHhk9lK4hDAobBTi4mXlxnGwJ7q9M8bBQloF5gEDYj4Gt7ZiqFGdpDngLLv6KggHPP202ImXIQouASUQkE15xN1RYo4BGAApwP4FIYPMnoIVYbKSCAfbQhNtlhCoW5UByxA9IE8qxjpapOp2ueZhJPtkatms0dZXLj0tt886xnpU2dUtN8j5sD3/nMaiRrHQB69kRIO9QP71b50MZV6E6MG5/NlLdnaTWH6hbpcAdYGIVEOAcc25k+yty6OIP9HNIhSN0BsojH1pzxbbg+0/bSx7DIrjRfwTPbsCVEikD0uMdvnUvggljM7RqWA5g5xjuNVPWuuUn4fEEDbwIqdazsZQgAPEACe5cdg7KtmcX4ZxZ1dccuLGw517DnrGJ/jnXkww/ADgM/CBtsN68tQCxOezAAOcDeorsaXYD/KOpS0AwCSkY2/pGoc6KYa16QOP/AEZ3/qUS/KYv0J7gkB/vvQ10SCro+vMgAU2rYAHLOKyezp/iPSfkJPqwfBqF7rfWrr6y/siimUfQSf8AsfstQtcf7Zu/rj9kVDIY8opjUf5CfrrT60xqY/Ef66/fUiKalpsaRShUss8nOWqOafl3xTBpDGXrwDYUp+VcBsKBES4Aa2UAE8LyEg19SJ1iWsRZMARJnJGPVFfL0q4gnYj0eMgbeJzX1KT1dtHwksHSMAA4IGABj2104XsPULpHjgiEYcAggsuTUZzKkJYY4A2Rk86ldZEiYjRwBsMDt7dqYmkJt3Ti4clhxAcvP99dFnMkWNuuLAA8+AZ+2mLMfjlwPq/Cn4D+Inl6vZy5mmbMfjs/kvwrKRtEy75R0La1e897fIz/AEqCsucD51bKpzi0x/dFap09juJ+mclsSvzeaCOMH85S06AYHdzrNJ9Lg07WLuG1M5gheSMdectgbZOO3PYKx8s6JP2o0L5NyE6WqTjPzWX/AA1rMrZTJA8cD7ayf5PCU6WxhhztpgRt3DatTyODKoWVztt/HjXTj0cWTYrqw5DMeYyTntro1fquBXXhzv2YpqMqythXcgnbmfLFKCoiBmWQYPpDhJGOzfHOrbM1FjksgjHDxYVjggDc99PwFHEhT1ezbHYKhS4DK8LArjOc7fDFSNPBWB1OdjyOO3B7Kk0QuFfxuQ/V+FAvTcfQ6yDjHVp8ZKO4Bm7l/q/CgTpwAIdYz/w0P2yVLKRjWtJ+LnfG8f7Vb78nMCP0F0+QD6UGYAkkY+lfasG1kZgA7eJNv61br0DWSLoTpnDxqhEjHgx/xG3/AI7qmGzSWgibJt3znIfBz5mmlX/VtyBnPA2wp8jNu/1+zzNJRS1jcKOZRgPcaJiiYN0yy13Kcf7+b4moMA/Ebfuwx+2rPpiCLmUdvziY4/rNUCEfiNv5H4msIaOjKeKMW0X9JJ/hpb7FB4/dXgGLSE/zkn+GvXG6ef3VRiJkUdchzyjf7qKuhm/SqzxtgNj+yaFWybhR/Nv91FnQkf8Aie2bOMK5J7hg1UNiejUElZVXifIIxsfvrwyRtwsGyANidyPb7abEWeA3AbGMLjkNhtXrPFnIUb8yoxkfdW5z6FmWXJykgTOwA5gdlL41PDlQQeZ4sjtH3UzHcJEzNFggHGe4/wAfGmxdBVMZwIuLIXHbnPbToOi1gKdZKUHIb+6sW6UgfhW1HLFog+01s1pv84IGAT79jWN9LRnWoAOy1i++s5msdARq11PZmJoXKB0RWGAeIcQ2INfQunqw6KaZxcL8NnGwaNfSQ8AJO55cq+dNdb0rcHb0U8e0V9EaFemLovpMRGess4iByPqDOf31MNl5OoomR3CXsAWX6OUDHGADxDxpSK0XA5kDKfzx+73VHdFB4VQBjuRnOc09bKQAxCeln0AcZ8edaypHNdkgSrJKCjIM8xjb/vT1sR1rqBhQeec5OKjr6UjAhQ2x7OQ/g1ItB6bPkniHM86zsuLAj5TWAhfIz6EP7cn7qHOjX+xukDEY/Fgv7NEHynYKOudykIP9qWqDo2vDoPSLtxGBnv3QVm9nS/iKm/JS+cH/ANZoWn31i8/pB+yKKp/ycv14R/0jQrN/ti8/pfuFZshj6io+qfyIeMi/fUpai6r/ACJf6QfA0hIpq9rq6pZYl+VMtTrb02wqRjLV6OQ8q5hXuNhQAzeiM2jxiQdZxsSgOTzPPHKvom1uNZu7SApY21jEqLhr6fjf1R/u49h5F6+fJ0VdOmVVwvWuMAbbGvpO2gNzBCkTekY0Jc4AT0R2cz29wrqw+RZr6FhJQiia9kdzuWjiVFHs3+NIltQsFwzyzxssZ4kLDL7HcHFWJ0uFUx10+CckBgAT5YqBdWyxRkC7L/qsik491b2YVQ7BZSi2z+ELv0RgjiQg7n9WvY0uGluRbSxxzcK8LyR8Yzg8wCPsxUq34vmbFvWIydu3JpiFuruJm7wuPcaiRpHRlXTCa4tulcb6qkSyJ1RM8Ds0QHXIckHdAMduR40OajYSNrmp3bzW6W0k8kit1nEzL1h3CgHPqnFGHTcEdMSW3wkB9860EdIIZTLrOn2s4ghMsyoAuREC/pBO4HcEeJxjNc0X7mbzXtiW3yQqsusQ3CCRTdrdXLBtyvEdgPYB55raV6zLCJFZm3ycDt51lfyfKB0ntgHVsW0ihjsDhQPZy5dlak0TKCilccOQeIgE9mO+uuD6OSd2MGSSIycJ6vhbhYDltt3U8GnJIPExZewjBzXmX4p+HJdm3Th9bv8AKnFj6tCOtBDY9EZGfOqJESOEj4mBXft7af0/DJKQMDiO2Md1MvxcBbgBB2HbtnepGn4aGRhyLfupBHYuHa7m/q/CgXpwMwawP5lP2no7h3vJx2AL8KBumg4oNY/o0+L1LNEY1rRKCM9nGmf7Vb90GkVugdgh9URyLkHudhWDa7GXiCjPrR8vritw6CMX6GaeAUyvWqDuDnrW2yKmGypaCOMH5jvzz95roZEVOqOcurYwO4b/ABr2PJsRnn/maVAM274JGx5USCJhHTMZkfH/AKiYZ7vSaoMUY+Z257SrftGp/S4Aylf0ppz/AHmqNGv4ja/Vb9o1zx0b5djYTNrB3ccv3UsoAUP8eqKUF/FLY/ryfEV7IpzHjfc/AVZkMcOLtABzRh8KLOh68HSSPhAz1cnPlyoWAPzyPGPUPxFF3RIcHSEE7nqX9m1VDZL0aC2FU8fEQuCMj0R4U4kcCjDASHi4mLjcDupoyyhgiqhYqNiR6IPIeB7acgSOaVjOPQVSAoYkk95PIDsA863Mas9ZYphzRByHoYx4Zp1LK3t4lafhmkIHCpXbbkaat4mAIikG++X5MucY4vdUxbJVPGWBcEc9wB5CgaQ5aYLSER8APdyPiKxfpVg64mOYtos+41tUCkSS5zk9/ZWKdKBw67//ABov2aiRogB1xHE9ruWwq+3lX0ZZM6adphkgRUjtY0AQ5OOAdm3/AGFfPmsuovbftCFOLw7a+oLERXGnWrhcoYl4QR2FRUwLmrSK2CNSHK8ZxkKS2x37v45UszBmQtg8wcL93dXrIIbhliljLocHJzg42yOw4HOvcq5HFknIzmqezmfR2D1it6wUniGN9u3FSbPOHXDYBPOoqsVmDdYArKT3Z5jGe/8AdUmz4vTz4YyN8UiogJ8pYA64nt+bge+SqPo9/wDjvSHuAQA/1o6vflJ4dyTuZIRjyEn76ouj23RXXu/jjHvZKy8nS/iezepL/SRf/VQrJvq95/TH4Ciu4Hoyj+eQf9IUKup/Cd4x5GdgPHHOoZmyQtRtV/kS/wBIPgalINqi6t/Ik/pB8DU2CKaurq6kyxBptqcam2qWMaalnkPKkNSs0ASJur+b3PEW2lkY+hy35c6+gE1QSW0CzRXNoyoFBuIwRjhHJlJHvxivn67WRYLj6RiOtlXhdVOcZ7cZ9ua+hrE9ILS0ila002+jEK4MLtBIdh2NxL/eFdeHyGXtItLaAtbB3u2K8/onHD7SKiXUAMLt1k0ThsBWYsC2dj6X3GoDarpk1zxX2najpEgzm4eJo1P/ALsZK4+sak38k0FpHLE/z62kcMjRFesx2kDPDJtk7YPnWphRa26stqyuwZgMFh27mmbZM3j55BVOPfXmm39pfQSi2nWR49pIz6LxnuZTup8xTtuuLuQ/qKPjUSLRl3yhkx9IrqRea28Z5/zufuoJk1T8MXDzS2C280yFncEkOMD0lB5ZJ3o2+UJlfXL3GciBQc+ElA9nGS1gG2zYnPuWuaL90v2dU17Ihr0JVY+lUB4AxaGReE8j6Pb7q1ASBQ/VdUIyw27A2O6s26IJjpRaHP5knL6hrRuMpGWUArkDniuqGjim6Y31jrKXUsCdy2Njt++lIA5PGTyHbtmmrjiErMOPhJ7eX+dOLI0kXEY0IU4PokVoZ7YlYQpMatnPq7/YanWEfVwupxnPZy7KgyEkAcY4Qcctv4zUvTM/NCx7WJH2VLKiPQfy2fyT4GgjpngW2r4HOJc+fE1G8A/Hrj6qfA0E9LV47PWj3IPi1Sy0ZBrEUs/BDAAZmZOAHlnizvWvfJ5Itx0JsmEg62JpFkVTsG4y2PcwPtrMJFUajauTynj+Joj6M9MrbQeiNxZiC5fVZ7mRLSFYuINIwUJk5xz5+FRF9lyXRsC72vLHL4mvF9CymPcjfComhrqg6OWa60YW1MRKLkw+oX3zjFTSAbGcHkUb4U5bEjCOlOTc5/XmP95qZRfxG1+o37RqV0qT6ZfF5v22psDFjaf0Z/aNYQ0dGXY0F/FLXzlP2ivJFxKo8/gKeAzaWvnJ+1SZ1xIvt+AqjEaRR8/Qd8Z+Iot6KEDpESRkmGT7qFEGL5CeyI/EUV9FwRrbYIDdQ+G8aqGxPQeiN7iExYHAo4pW8dsKD2YGKW8E8sSqWCMkWccGCBnl/A91OBjHEqKOFQMcQJyx7T2j7Caf6iaeJY1UxoclpWPpDI7PHfmfdW9mWyvjnYTnrJ8KgwR6/Zn82psUzKhkWeTZcENGOFD38I38Kl/MrdVEaQqFRQvpJkEd3jVdLbkyMBAVdAPSUEDnn4U9j7RYW7MVlYyLIQPWAxvisW6SAtrj5/8ATxD/AKdbFZ5+ZXI4g3rbjyrHekgb8Oyj9GCMf9MVnMqIE69Fx6hCibsQp88Ka+j4VvbRLdEZXURJxIpwQAAOR5Dny7q+cNYmCazHk5CoO3OdjX0tO/WxxGNVmHCAFHlzPd76nH22Vk+KBO/1B9L6b27yvw2+oQrDJvydWIVs/wBYDyJolc8Ex9UHA5nt7cd9DHygaeW0e2vgE4rWUBlQk8KOMZz274q+0m7Gp6Nb3THjZ4wr7/nDZq5oZGvUTxS/a/8ApzEmNWWUcQHq74xkYFTrQHLlm4jtv/HwqIpzKSCMDI32A8M1KsR6Lbg7jYdldXZcDPflI3mIJH5eLHhhG/fVVogC9FdcI7Z4x/eT91WfyiMBeb7k3SAf/F/nVPpVxHbdDdWeVlHHdrwrn1iGBIHsFYzko3J6OmTqAq7uVilnjIPEsgkYgcl6sAe0nlQzI7PqdyXABWQqQOQxzA9uaurdpZ+ITbkS9Y7ZyWkwAB5KOzvIH5tUY/2hd/07/GueE3kXIwT5dktKi6t/I0H84PgalJyqJq38kj/pPuNaFop641xryhliWNNtSztTbHapGNkV6e6vCd64negB9rk3dnKrr9OvGz7YztucfGvpSyuD8ys1YMCYUOFcbjhHZXzrq9o5ee6hz1olkV1A5jffzFbl0U1tOkfRi0u4QV4UEUqjdo3QAEDwOx8Qa29O2m4yM8kmkovZeTyyuvAzSjbOMjfz238qobjo/ZJK1xYvcabKXBaSyYJ1n1o8FD7VHnVwoniQn0sZO+cf9qR+UkVZXYoxwTxYIONx3bV1GdlFdQ6rGqz6rpB1JEzwahpTGK9hHjHnJ8kY5/RqTo2t3E5kl0+7h163QBZUAEF7Dz2eM4BPmEPnRRbAC3YBuIAnDd/jUC+0HTtVu+uubcC6RB1d1CTHNHz5SLhvZnHhUtmiMt6Y3cN5q2ovEz8XUIWjkQo6HrGOCpAI7PDlQvZLj8HKR/5Dl7BRH04jlt9YurfUJTdERIlteMgV19NvRcjABOSAwwG2BAPOhs0lW401SOtPzInhICkbDIzyPtrkXyZ1ydwQcdFV/wDElmQN+B8f2DWghzwEAEnYk9uc/wAbUBdGMfh+zIByA2VIww9A9lH78b8O2V25eZrrho4MmyLJIQ6FsZJO5p8yLJlnOTgcKkZA51CuELSqFUvwvjYZ3B509EUK44DkHBHLG/dVszXR5J1ZK9vpDiAXHh2VY6aqrbFVDcIdh6Rz3VBDRrG44Bu2cCp+mKBZDYAlmJ99Ky47Fwgi/uT+qnwNBnS0fies4H+7U/a1GkP8uuPqp99CfS5B8y1fxgU/a1SyzJpFL6la4BJ66PAA7eKjf5OdHs7iP8OzpI2oWry2ilm2WMqvZ38xnxoD1VpLeJJInZJFZSrKcFSDzB7K2LoavWdDrJpJHeV5JS8nCAzNxtucdvjWcdmj0Ey7wHHafvNJY8OnTsexGP2GnEXEQHcfvNIlwunTnHEOrY479jVPZKML6UsROrbHDS8/rt+6lcGLG02/3X3mvekYZ2TiThZjKSuc4PG21PBfxO0/ovvNc8TpykfgPzS08pT/AHqTOuZlHn8BT7pizs/qyftmkTL9MuewH7qswGY1H4QUHJ+jOPeKKejCgay5bdepbahyFCdSXv6vP20UdG1I1VyOyA7HtycYqobE9Bu6rBIUmCSMwyIx6xOOQ7qlwWjDq4Jp3jwCRFGcZHeW5nn4UxLFFCqtktckBm4iRny7APOmWupUOJDhgTwljkjyNbmV0WrWECqOqQo4GFKuVI9tRZrG3gUfSSM44cEsS2c86Ya+cHJYlVGN+WPE9tRJtRMMqN81uZYxuzQr1hUeK8/dmk3XYORbRr1en3XBj1WK48qx3pID+Hbzb/dJj/4xWr2eu6XqFrcRW97C0/C2Yc8Mg27VODmsp6RNw9IdQUg+iqr/AHBUOSkrRcQA10f+IkXsJUDz4f8AOvpyJX9BoFi40AGGBHZzONu+vmLV+KXpnZ24Jw0ybg4wDgf5VtXSbUb7ol0gF5blpdKuzxSQvuqyj1uE/mk4B27c7Vi8ixRc5aKyukgv1KzbVtMvbaWIRLNC6Bc+kTjmfbigb5ObyR4brS539NfTAbsYbN9x9lHenajZ6/YR3thMCGUgrndTjkw76zy+Ruj/AMo/WKuIrhllC9hzsw+NcvrpqDx+pjpP/hmEtphvNJ836twEKPLHFxE4By2Pvq3tE4OsXBBDbg9nKg6PpVpmsXCWdrKRcpfwoodfysay7sp7vCjeNQCSpJU7jNegmpW0+ioozPp7H1uqFATxdcSqgZyRFH+80E8LuV0+ObiWN3lkmPIHPpPjuXZR3kedE3ykatFZdIXhQubogvwqPVQpGuc95PojxoI1S6bS9Fi0+FeK/vH47p1/NVfRWJfDOfPhryfUPJOcovpJ9f5+/wDOiMs2/b4CjTzG+nxSRKVi61o0BOTgAcz2nLZPjmh+P0r258ZpP2jRLp9o9lotlbSjEsbuHH62FJ+049lDsRCXNyO1nkPkvEfia1glhxJP/LNF7YokryqJq38kj/pB8DVgIuri45Obeqp5+Zqv1f8Akcf9IPga1jJS0UimpJNKNJNUzQQabNOGmzUgNsd6VSTXtICwtLpnsJZ4/TtwMsq5ZoCc4IHNk95HjR70cb/Q/pPawRzrJoPSGJJLWcMGRJcDbI22JI8mHdWV6JJwYhtmbrJI2aANnD4Hpwk94G6nwHfWsXmgxa/0NXUOjIaa2mVZLnTQQpW4QYMkPYkwPNfVcHsJzW6i7/taM5y5RX2jTiUTJYemNgAABny7KjRwfTRdY6FSfSD4Krt9vn31WdDde/0m6MWt+o4rtAYLrbDLKuzZB5E7HHjVsUcS7I6uGzhFX/t4V0J2rILGzXq4XTi4grEAju2pcYzcMf1B8TSLLJhcuCGLHOcc9u6nY/yx+oPiaT2aLRk3T9V/DF8JFBVoFUhuRy5/dQlYGRLzThK5cG09B25749Fj9gPbtnfmVfKCxl1i8EYUcKx8Rbs+kYbePpA1R6XETdacrDObEjJxg7bjFci+T/Z2SXsTDHRrZJtXskmTKYOx2weA9vMUXGK4ixiUzR45SN6Q37G7fb76FdHb5jqlk8zE2xAxIeceV9Vv1cnZuzkdsGi+QjjVljGxwN+RHeK64aODJsYcSSBHReHDE4PPnvtUiEy8AIi4iAAeLY03ChRgHyXDFsHYgbkVIhkBJCkDJ3ydyfCm5ECHLoSWj9Y4ODkVI0c5tHycnrX39tRC7xnigLlgclcAjGfhU3SFxZZHJnY/bQi4odiJ/CFyOzgT/FQx0pAax1bHPqQPtaieLP4QuNtuBP8AFQ90lUNZarjf6EfFqGUY5rwxact8rv8A1q1zoch/0QsQCfXmzv8AzjVlvSCPFsBg815/WrUuih/8JWXCMDilz59Y1ZR2XLuKCmLeAfx2mkOM6fMMZyjbew0uI/i6nsIFJk4Tp8uTgcJ3Bq3slGJ9Jf5XHt2y5/8AkanAn4na/wBCPiab6RLxXK77ky//AGPUrq8W1qf5gbe01zQfR05tjEkZ+a2eO2Nz/fNNTxnr4wRzBz9lTnT8Wsx/NOf75pu4T6ZNuxvjWhgRYl/1gO/qx+1RT0XUpqjkgHEHb5ihxE/1jz/3YP8Aeop6L4/CE+f+D2jxqobFLQWmTiYdXNPywNyxY9vCv3nFOwW90I5DxFeIbmSQbexf30zkRvg5jbY8RJO3dUmNI4/TaUqrjfBIznu7fZW1mSYk6ec8ZkZiSMFEG/8AltzrmtJ+vUAo8eQ68TkEkHu7x31PSSCE7EqH3HEDj7ad9GRQwII5gigqik1LRdN1OxuHvrOOeWMMVkZOFwcZ2PMe+ss1eCKHU76H02WM4EkjF3IwOZ2J+2tnmVXhnQs30u3ojcbYoXu+jWjXlzctMs0c8pySZeIg8vVHlWE4wb/spRbMQu9HFz0rivevXq4pYjMEBYxqCCSQPSGw7seNb9epo3S/QZraC8hubdxxccDKxjbOzY7CPHnvQs/yT2J1eDUhfuJIpFlMYXYkHPfnv8KI9Q6DaLeTm8giaxvN2W4sn6pvs2NJRnTT7Qp3+zGo9U1b5Pukc1rKgZcgPE2eCROYIPYD2EcqNuk99Z670dsekOmsxNrMBJG3rRhuw9+/b40jpt0O1q/08LJMNYECnq5TGqXMQzvy9dT2jnyIrOdAubnTtXTS7u4NtbXX0LtKMIVbbD92+N+YxnsrzsuNxTw+H9/5/ucrbi+Pgk/Om0XX4buB+JophKCDjOTxD3g19EPewWOmzX10wgtoYjK5P5qAZNfOfSewkt7y2hmUpNbzG3k8uLY/a3uFGXTr5SdLktF0iylMkDS5F0ql43CgYY96q/Nfzio7Dv0+jn7XfRpjdWDOo3d9rGqXmtToVuJpvRUj8kQPRT/20OPrsf0alTxW9v0kiPAsjqwWCMn1pCdie4Akk+XjVrqtxpVv0UtH0hpbjT0kMcF1KMdeSoLtvv62ck9pPdQ50Sin1bV59Xm3gtSsak7DjYHHuVWJPlXDKOXL6hwlpMinyoL9WuksbOW5lPEEuJyOzibIA95oZ01QkRvrveW4PWIg2JXJwfAZzv7q68uh0s6Qiyt3P4LtZZJZJF/3hZuz2YA9/bTUUjSzOzY9YqAOQAOAB4ACt8sPzTq+kafN/wBImNI0rl3OSfcPKoWrEfMlHb1g+BqUpxUPVz+LRfX+410xSSpGqKcmkmvTSTTZYk00xpZNIapGNknNLpB50rnSAhaTFDd6rNpc8zxtIC0E8Z4WD8PErr5js/WNal0X1bUdCv7mTUIm6+OKL8LQxqcSRFfo76MDmQu0ijfAz31jAZ5tJ0fVYDwS2sws5mHYQeKNv7JI/qV9AyXttqGh6B0xtnEHzdFsr91wTCpIXiI/m5OFsdqsew12LdGXVUWmt2d7peoRdKuikcd0blh8/skcdXfpj0JEPIS9gb87IBq+0jW7PpRapqWmOssRHVOHyrRMDurpnKsM8qqNISXRma3ERTSZ5TG8KnbT7nOSo/mXJBU/mlh2NtYT6IltrUmt6ZCI7yVVS7gBCrer2E9gkXsbt3B2ORfYBLCCI2zw8Rznh5dldHtNj+bHxprTLmG8sVngfjjbPZggg4IIO4IIIIPIil8MgkZlbfh9HbYCkykZT0xjP4T1ZyoyVB7yfpcYHdsB9tRtJtw8+nsVH8k227Kuel8Cy3d/sASkbZ85GFJ0mAE6cQM5tDjA8K4VK5v9ndJf+uP6L/TYMXlqAo3GMH6pq1jX5qSjhjb4wO0xjuz2r8PLlGtIistsV5hRj+zVgWaMAso3OCcb8+VdkdHnT2M8aS8fBldiRj91OLGw4hhcDbixy5/vpmNSASFUI3sxvUuN14Mjh3OD3f8AamSRSwKKpZiMH0gOW/8A2qx0tXW0w+OLiPI5pj1MAKASPzeXOpOnkG3JUEAuedOLspDkePnk3fwp99UWupm01QfpRD4mr1P5ZN9RPvqo1ZOK21EDtQfGm9FGSdJYSLYnB24T/erSuiwA6JWYIB9OXt/nGoK6UQFbAnhwTwjfzNG3RqMp0atQQcBpeXZ9I21YrZrVxQSRL+LIOfKmrqMSaVIjDYjsOO2pEIxCnspEwzYSfUJrSRC6ZjWvRj51H/7h/wCo9TGTFpaDH+4X76b1tczRnwcnw+kepsyYtbT+gX765cejpzbI0ifQWQ/mW/bamrhPpkx+ifjUt1wll/QH9tqbnXM6/VPxrQwIaKTqOw/MX9qifovGPwhMXOFEQ4veKHo1xqJP6iDP9aiXo3HjUJAFJYovCPbmrhsUtBSxgmlbjYRRHYBVyWHeSRgeynreJDMWifPYeeSMd/dUnCXAIJkjZdimcY/jvpHW9XM6Rw5GAeMttnHdWxlRLY8K5IPsFNkAEsvbz8fZTYBkYB24jz9FsAe6kEgBkYk7nI3ye6pm6Rce2eXUsaIetlAXmQG4ao57mchvmyLb243MjDAx345k9wNP3GpRWyF5bJOFM8LHGSR3DmfOg/VNcuJITqV0eBOJhawDbJ/SPfjv7/KuRy7OqGN6J95ros7kB76ZIA7wuy4JYqBxHPZgkgdmxq56N9JrbUEFssrNJvwcTBifDIrK9UMhsrSFmJcIWfzYljn31D6CG7sukVwzSOUjuY2UZ7CRt8auEndjyYujcymZmdweHi5KN+XL2Yqk6X9EtN6S6WVu+CG8wOpu+HhKsTgA94Pdz7qvtQ1K10izaS+lVUX1dssx7AB21j/ygdI7/Uobe2SBw0zcNlZIOJs8utYfnNvhRyBJ7qefNCNQfbfg8+VJdgH0r1y4i02LRrgrJqFoz29zOkgdSiN6CgjmRvk92B31Gt9Il1K/stOhglnnihVSiLkgnBJ8SWbAHIdvKrq9+T/Uuj2mDVNatxGxbgEWzCMkZUg5wzeHLJ7an22mTX2p2rWV4bJdSmlbT3EuV4o29GOTHqs3DxZPaQfLGu6SMuLIWp67b3PRX8Hma4a/hkAlEkYRI1XiTgRQcAKMDvOc1Et9VnToOdPtkMenLL199cEYM87ghIFPdwgZxvjPIcx7Vbky3947kJdSMxmj4uLLnPEQfE1oGiW9pqs+i28Uxn07SII5FQoFElzJwliQNjwjh8STv21MUk5SvYLtk7o3pZ0rRrfrP5RckyzDGMHOAP4+6qa2PpMf1m+NGEhJEJJ/OkPvc0HW3b5mrUVFUjoSpUTAaiat/Jofrn4VJXxqLqhzbxeDn4UFIqTSGpZptqGUIY02xpTU2xqRoQW3FLBpv84edLoEDWgXY/BGt6e+MTW6zx57JImB2/ql61X5JNYt5L676Namoez1WNo+BtsS8JBH9ZcjzUVh9tO1tMJF7ip8QQQfsNbB0p0mXRbzStbsW4GuLG1v0dRsGCorN7HCE+EldWRNPmvBlP7+jXNEuZ7XR5U1BusfS5W0zUWcbSxDHVzEfUZSfAt3CieKOSIshwyAAKzHiYjsB/f21Q6TqkGoXFjq0cQay1+0CSJjIFxGpPCfNeNf6gqx0zNgZNKlcskI4rWVz60XLhY/pJkDxHCe+tW7H4PLtJ9EmbWLQNNav/tCBBksAB9MgH5yj1gPWUd4Gb63miuUjuIJFkhkjDo6HIZTuCD2ioy3kFnYNLIxIDYAUZZiTgADvJ2FUcD/AOi9+pxw6FeyerkEWEznlkbCNyfJWPc2wNFX0ojX8I3uF2MUf2SE12lQelpwA2Fswwef8bVe6r0dlv7qaeO4jHWIF4GU7YbPP/KkWuj3lpPaNJGjiKAxMY3z9hxXB+Kam3XVna8kHBK/BNhjwYGxyAOPZTkoZyAEZVB7DzpxUK2iZjbiCDbgJ3xTC/pNlCDjccO1daujib7ES8CSs3o8Odi/Yc7j+O+uhQxoCpwM5yN+yuASYniAY8yeLGe2pEKIsZWP1e7jz2VRAwsiEbMBkEYJ7M9lT9OI+agDkCQKrpI1EJL8LBdxz7D39lWOmLw2MYxg433zTQ0haEi7nY44eFe3lzqDqChobwDtUfGrBB+NTeKr99RLlQ0dyBnkBvTZQB9LLfOlttklkGP6xoo6PgLoES4wBJNuP6RqrOktsW09V23dMZHbkn91W+k4j01F2BEsvbj/AHjVz32zb+KLuPBiXHKkyj8QlB/4bcvKlDK22VwSBkUwrs1tKjAbId/Ya2ZmZVrQEbxEBmJiYALzyZHqSjvcadayOvAyx8BXngg07rMI4In58Iz/ANRiKfit+qsUTB2L4z9Y1yYn0dOfZHkTayH8x/iamZ1+nX6p+NTJFA+Zcv5OP2mpmdM3A+qfjWpgQ41/Hz34i/bor6LIBfsSMnC9vjQ2qEamAO0xDbs9KiXo+Px2RTnh9EZHnVw2JhXdTxAdWXPF3ICW+yoI64rgRcURPo5AXiPkKVqmoadpMHFcnYZIhijLM39UUD678pF0kLLY2FzbIThZJrc7+/AFdUMUp6RjKSWw+KTpKOJTwg+iYzgAeX76Huj2pz6lqmoWVy8zvE7SEvsF9MjhUfojAx5Z7a+fr/pP0muulUdrpet38JvCBKy3D4DZPE2M4GAM+yvoro5+PXC6zE8T2s1oqRkDD5BOc+0N29tZ5sTjV6On084cJp7a6IXSnUbfTADNJEr5BSLg4g57iO0eFZ8b+01W5Mkt21xJxleBo+ABl/NI7AO4UadNY0uW4g+JEOVx2UEaRojalqZcli0X6J4QMncnzri6tnoY4NRTImoArOXuLhFycDibnUvo7E1vq63DYWFJPnDSdU0n5NCRhRuTkqcVTajpaS668j5kEDsF3PD547a2Ho50cgi6LWduyFZJrdWkkB9MZOceAIODirUW/js5/UzcY0CtrpGudLZzM5mktwxX5xqR4MDOfRijx7tvOmbfoXpv+ll2BqlyyW1vxSTQNgkk8IRRghVBznnk+2r3XTePJF0ftNWlhcxtcXb26LCtpbqM4wN+JtgMty3ocvda0joz0YuhpEZQyvFZi9ifLSFstIFYjfhUHfvbkBisUksijLt7b8fo8ykVvTyy1LT9G4mmnuNGuAqqJ426yIjPA3EWIPPsxz5DY1JZtPuvkWtb6MRh7BIykKRHhaRGCy8ZxglsnnyyO2o2lW1/0qiuWkv4LPo5wmOW+lhDySkc0jZ8u4GBlthscAcqCHhlstNvrWC5F1bTuW6xBKsLxg88EADiIBxz9E57DWz6bddMpK9DeqaHKdDh1bq3CzSMocgAHBwuMd/CRvzPZgVb9G9Zs9E0SC6E4kSPAkt0jJkLZ4mJOwUcWOecgjxxIu4ZrDSIDqH0cN7YiXq4U4Y0bBQIVzgMMZ4+eTv30KwTNZDF7CTaXseJVX81sesP1hxbjx8qy9r6+iWq0ahbXUd9p9ndRFurmjMiHO4BY7HxB29lCMaTs/FHcJEmchPm6PgeZp7oQ0kEWoWbTcccbLLEAdsMDkjwJFeW3qg+FXZou0TVkzEiNHCGX/eJGFZvPG32VE1UFYYwefH91SFNQtUZwY+LdHPM9jAcvaPhSGV5ppqcPKmmpMsbammNOMaaapAQPXHnS802D6YpwUAZ+InIkOD9H63hvj419KJdabqXyTdFNRkIuBp0USXKFW9OBh1FwpOMbA580BrGbmxgPyjavpMRjEN5NPBEQcgFsmPf64UUdfJBLa6t0U1rQ7pA08XEYskghZEIPuZftrtlKlYoxUnTDPoxayafZ9IOhwu0kudOmTUNInkPDxjPEu5/WXhb6zVoI1G1utMh1aExsOBZ1QOOILj0l88ZHmKzdJYvwN0V6WqSrRQLbakqykO0L+gzeHBIA3tNFOmWFvDqmoafPKymOQXVtwyAhY5c8SjI3xIH9jCsllpaKjjWrCDV9PlvrTrLNg3EFb0Tv6JJUr7z7DVFOZrmNtNulKW0cfVPbg+jKSvpcZ5sN8Y2HfU7T9Mhgma3WZj1DqY913jO6g+W49gpE5SSeV4lYKJSCSc7kf5UnO9DceJCsdRu9NMdpJPLKiLiJ5GyWUdhP6QHvG/fRLZ6wJgOI70M3kKyAq3I75GxB7CPGo9vLJG/CxHGOeNsjvpKbTFVh410AvEDtUX8MRiUxtzqttblpIipPZVFfuw1BuE4JQH21TyOhKIXtdWkx+kiQk9vI++noxZlQACB9Y0FRXblcMdxUj55MLeQqxyq8Q9lCyMOIWmK0KlQxHfg0/C0UacKvxDszQMdUm6uGQsfSXenY9WlDAh6ayi4huOEOX4hhgB7qaaDImwQesOcUH3Gtzi4VVOzIX8iKct+kjP6LH0qf5PAcS21jTbi8to0hg4isisfSUbDPjT1vaywQJG0B9d27+bE9nnUeHXAY2P5wGfOut+kkU+OW4yPKlUbHbqi9UYgA7lqPK4SxlPMlHwceBqLJrEaW0kyn8mONh3r2/vpNtr9ndoQGB7CDV2iQV1CNXaPOPVBx48bGpeoxgLEdhmIE/bRFK+mGNZJLeBo+IKS0Y9HPL7a6aw0m+jXijXGMAoxXHuNYxxUtm2TLy8ARNjNn/y4/aam3GbobbcJ+NGMug6KvVdYsgCrwI3XNyGTjn41x6MaW5DrLOPETZ+NXwZnYHdWx1KMqpYlkGB5mpFxrtr0fhZy7STMQjFMcKkZPP76la3BbaC8jx3EkjFfzgPQJ7iO3FZN0l12O847eJZ7RpBskowvhg8j2bV6XpPSpR/Jk/0OXNlbfGJb6p8oml3bMrm4If1mRwwI8VNZtq9r81vHvNFuX+YTelwpIfQz2YHMc/hVLdXDGR1eMI+SGx30m11afT3YRsCpGVVhkA+Xj+7urolO1TIhGtESa6lSVWWRgwzuNs19DfJB0vQ9Dobe7fhRJ5bdZDyV8h1U+YZseRr5zuZ2ubh5nADMcnFaB8lF9HJc6poVyxEN7CJUP6MkZ2I8cE+6uPOuUaR14mou2a7qd71j3pHpO7DhPcN6E76VrDheWxcs2D1kTcY7+Wxqytr6402aS01CEy4XZ1OTjvGeYqFqOr6dCpeXUYbfIJAkfhJGccuZrylFp1R7Kyxq7JnRmL8N6vbLMXKzzDjEo4Tw8z7+XtrSumnShOjWnIIUWTUJ8rbRnkvex8B9tfK2s9Mru61FvmUrJZpsikev+se493dWqfJZezdNZ59X12cznRlRWLnJkXBMY94OT24Hea2yxyY8Nw2/+P7PI9Tkc5e0JrfS3tLCVNVmkc3IW61RwuZZHYgRQg55kkbY2z3AUKdOhpUmmw2b36wy28MtxbQxJ6Ej8ax9Wn6qhZPSHMgnJzRjdySX+rXnztza6PpOZ9QvH2LzMuW4B3hTwr3ZJ58NDUdp+Ejd9NL3TlgsZzFp2n2jrslsQyFgOw4zjxJ8K5oR4RcpfX+f7f8AdnNfVF50dthefJPf6zJdtNePpk1vG3CFW1RAV4EUYAJxljzYkZ5CgK3it5+hS3k6NxWcwUFmY5jYYACghSc5JJH51Efyaag83yc9LdBO81rDLLGD2hkIP2r9tQ9GiWfoDqcCWwlQXZgJ4uHJWNBjfnksAB8KrJOVR4l432mWIktn0rSYLpgbYacsqNMNsjiJJz2cOcn9WqKx0T/SHo3aT38jGC7uZks3ReFoCpGWxnHp53H6qjPLFXqd3d3XR3SNMSP8clia2CKeSRkknyxj7aLNDQTdDtOtkZo4hK5iOclMpGQfMHepSUZv7Ztk+VeAN0JrnRtfTTrkKxKFA42DxturDyYcvE91T7Rg0YI5cqf6Q2qanZ2rIpTUIIyeKM/ktyGz4Z3HlUay2gVODgKADGcj2GtH0ZpNdE1ah6oOO2Rc4y3PuONjUtai6l+QT633UhlSj9YmSMMNmHcRzpLGlkAEkAAnnTbUihpqZY065pljSGJX1xTlNIfTFLzQBM+VCxSy6QQdILeJWV710fKjhLII3XI8VbHspHycJFZ/KBpqajCDZ6xEWiU5KnLHgB/roV9tXvSe3l1n5Nbm7WBPSuLW5VVcsQ7QYbG3IhSfbVLJdW3+gHRLULMM2oaTK8k0o24F644TxwQG/reNdUZpxsi/KNc6FaVYXPQ2GC8gaRXmuVcCWRcjrXUj0WHYO2rO20UWsVo813fia3m+azyrcN6cTkBHAOQBkR5HfxUJ6B04ttP054JNOuZMXdy4aJ0xhpWYbH61W1x8peiyWE8E9hqadZGUyqRnB7D63YcGoTRcZdbDB+jxhu4biLV75MsIyH6t+ZyBuneMe2vbpBGv6zycTAcuW1B918tHRn5k8F3HqcUxQEuLYMqvgEEYbv3oqhuhqNmt4q4WdUkUEerkbj37UOqtD5NjVxHnkKrpUwQeRHI1dSpmMGqy4UYrJjQ/YzYIqFrR+a6lDcEFopxgfqsBuPvHtp+zHpCpkjQTfi1ygeJ5AuD4g7jxp7VDKjhBYMBjNOn0LK4cKWKpnA7u33Den7uwNkwAYvEfVf7jSYZBHKGIBXG4PaO2loCHb9XPbDDA88U0q4fh8akQ6WbDiET8dud0zzA7vZtSHXhY0aAaldF1IRyeiVjGCeRzTd1bqp40O/hTt3bC6e1mBxJESCe9Tj76cuI+FcEYI2IpgIt5WjtJ5n9SOMknsFVsRYWsMsbequMjt3q30+VFlMMqhopAUdT2qdiKiQ6PPY2rRl+uiALRyZ3K5xv4iqETLS4621nLnC9S+T3DhND1jcSJBDMjHPCM+6rzTmWKULKMxuCrjvU7Ee41TR6XcaQWs51JVfyUnMOn5pB8vtzVCLs3jzaPe+l/uCR5jcfaKi2OqzwHBYmNt/KvIYGvNKvbOM4mlgYRnOPSG4Htxj21X2Aka1VZlZZFGGVhgihhQT3l88+izNxnKOjg+3B+wmk2F1cqyqJCUPeeQqPBCt5p9zYMwXrkwrn81hup94qJMLix0mOOXMU4YEtz2HcfHsrTDjeXIoEZJcItiNevzLbiZhxRs/C7k9p5faNqynpMylZEJzvup5g0b6dqyzaTfxBw5hcKeIA5U94rOOkZZZG6tOOPsXc8Pl2jyr6HJSjS0efFO+wKuXJcgkk957ajscr405OwZzmmM99cLZ1xXR5V10R1AaX0s026ZmVBMFcrz4W9E/YapadtVLXcIBwS6gHu3rOS6KNa6S/KfpccMtha6XcXF1GSolnPUiNvAKST7xWa6/rsvSDUVvJLeG24YkiWKHPCoUdmSTucnnzNM65dx32s3M8QwhYhT3gbZqBWMEk7KbdUdWv/ACK3DxW2qWvDKsd5cwKX6slCEDuylhyYjl2eNZHIyHh4FxhQDntPaa1r5Horm10nV9RW4nSAq8fVAHqnYJgFjy2Lj7az9VTxtPREtMPtdN10k1eDo/1Z/B1s5vL0Wal2lLENkjtI4seZz2Ci7pNaW2sdAbqPSwCkEQeBFBBQxEHhI5g4BGDWW2HSLUuik2Z7N7N5wBgpiGVRuOEndefYSN/VFEsfTa3eCXUJb8Wc6L9KkyhkkB5cRUYYdgPMHs7D5eOalam/l/0TjSkn32BfQy8l0/phrcdtGXF7ZyKF7PSAYE+AJqs6La3qEPRTW47HhlmF5DLHHI2FxISrN5jhTnyGTUnSOol6d2r296sFtcqDHcZyEVTxEN34ClSKFtNuriG/uPweAZLomGFCMq3WZXl5EkZqsLair/RnCXFomrcTy9JLoafdJ6RlRTwZUxZ9MrncZ9mR21p+hwSf6OabIwwhlndiOSACMbmsbtlGn9KBGsrRxqjozsMAjhx7uVbXo0TNo1r1crPEV48Z22ULnHmufbXQ4K1JnW/jRWTstrKqLvHcws3GVwxkCkjPgVGAOzh8aG4FMaqwJ4cDI7qJtRiaSxHD60cSuvmBn/L20NxsI41wGZiMqqjc/wAd9ZydieiUKi6l+Rj+t91PxcYT6QIpzsq7hR3Z7TUfUd4Y/rH4UhFW1MsaeamHoLGnphjTrmmGNJgcp9Kl5ppPWpeRSAJI9Ta36JQQlWQW4tDJFjmAQpPu4ffUHorpwc630cKu4S4KRLjJZHyox38hVx0h08W93ay3MTJbXMZXKt6LqD6JBHcQNuYKjNTEV9K1a21GIosmpQT2ZPD6SgHjVwewn00B586vHLtwZCIOhWrRaQsN4/00UssbhBxHiDYO+w5jvNe3kMLAhOMdnp4OfdyqRHxRm5z6jTFlwMY5DH2fbUW9inROJ4XQHkXwvxIpNN6AENZgB4lZcHh4SD/HlX0T0duTLoNnxeiJLG3nU95KKG+0A+2sI1CBruxLgBp4SBhWDF0PgD2Gtp6NTs/Qfo3xRuGjt44zhPSJI4SN+3YHfup45Nxae0UthFI3FH5VWXJq8isJHXEhVMcwPSPv5fYaalsYFPpKW82/dim0WmVdtiNCzHGBUFpzLeBwfQQnf9bt9w299ENzpaX+myw2zmK4xlPSyMjs3oOt5Z+FoZYTDJEeB0bmh7j/ABvUtNFKmFaOLuzaNjnbI86qZSAuB6xIUCpGmSpDZrcTXEKxkkYMgDYBxnB7KkR9G9QluWmaS2WJiWQ8TE4PLIx99XxbXRNpDCTEqR3HIzUeePBGPVPI1eJ0YmBy16g7wIv869l6NylFCXiMVbPpRkfA1X45C5IHUBR27uX8fZXs3pe0fbVvN0dv1i9HqZT+q+CT7RVbNZXdvtcW0sYH5xXI94yKnhJbQ7RWMWRuNd2BwB3mrS0vCYjA5yU5H7DUOModRlibmhDjuORsR9td1ZW5DKdjzppgM3pNtNywrZZfvqwtrlNQ05IZxxBcjxwef3HzFVvSUmBtN2PVTcY4xy4hg8Pnjf30jTTIs+OE8DVZJ5E72F5wud4zz7xzBq36uHUbSI+is4QJxjtI5Zqn1+Uw65BAVP0kCuDjZtzy8qnaTHLx4bZTyzQxnkfHHGc+i65Bz2EVRdL9YPAzKw4SoXBOxUcvvPtq46Qzrp10/XuiW8qBxJucZ2JIA5ZGD5k1lvSe51WdmkhtmngPKSFlljI8CMjHnXqegxqEHke3o5PUStqKIeka1w61NbtI4S7iaMcRz6Q9JfHmCPbVLrshLthid+eaqTPNBeLOFEc0bh1AGMEHNW2qNHdIJ4vycqhwMcs9ns5eyujlaoyBOdiWJO57zUepd0uGNRKwkdENHV2cb1521xNZOfRdHV2aTXuay5DPcjNbH0R6bWFh0Eg0i3jY3EED3EoYDhLCUN5nIx2VjVaL0RgnutLtuqtVjgVXWS4dFBc8WcJgZPZkk4rLM7j2TNdBz+FNa6S27Rrc2UTkEm1EImL57Hznh8hvXsWjRaPpNxqlzeQ2d1bBc2cJ69TI2wThYDhYjcgE47R3Uc+jWEk8UzWsamIqQIwBxEHIB78miLX7mTSbC0sOrPVLm5vpXRXR5ZNwrhh6QC478E+FcihFpuRlX2VF/Jb6vNpGpxJHEvX9RMsXo8IY4+9ufeKHLSC1temllC5TEUgcb+gxHqDI5KTuT3E1ZzQNAjywOotbkfSCM5VCD6LqcnkfcCRTNsunx9JLW91SMNCI5ZXX1hMFBMakDtLhVx4Yrmx2p1Jk07KSO+R+l8EyojM92pICkjhLAY58sH2+6tVhItQtuGiiiVGHUwPxYPECeRwDue0+VYpdmW1vZFCMHMnE5bnzziinUdMmkiW509h1g3CHBVx3AHau2VM6mzQDFGzDgQxry2csceZ+4Cqd7KCK1MkStG6ghxxE+kNjzPeKG9LurfUICBEsVxH+Ui4cY8R4fCrGOIq7tklWIPkaykCaaH81Gvz9DH9Y/Cn6jX5+ij8zSEVz0w5p1zUd2oLGnNMMacc7UwxpAeodzS800p3peaVAFmv6jJbaPqGmXjmaJn+eadMRhkbILxn6yHPmoqX0gmjtoESNszW6xOzM+yyrhig8OY7Tkk8jQfbdNLz5y2oXejwX+kqBGYLtOJWIUKSHxlWxg+idqINNtUnt2uURVaYEuCesK534cc1A88nmdzWs4tK/JHnosPnIMXHGTwvlgc42J8N/tqKbixCPFeWSsGG1xE7LIh7+ZVh4EUxFc8CJDIFVivCCQCCRsQD2dm1RLqTvVT7MfaKyxztWgI08DafqcSyur29ypQTJ6rxuOHPsznHhWo9BLQXPQ7SytzPY3yI8bXMDb8Suw9NT6LjwI9orI52We0eDjyyHijDcwPzgPj7D31rvyfvLL0StmdGD9ZKHyNw3Ec/v9taqrtDQZaPrc76i+jarGkWpxxdajx56q7jzgvHncEfnKeXiKtpgD21R3NqmqWcStL1F/aydba3CrloZRtnHapGzDtBPhVhY3k2oWMczWMyTDKTRqMiORThl35jI28MU6+ik/skQScEgIJ86Tr2mxX1p85QBbgLgOB2dx7xTbdYh4ngmTxMZxS5bwm34d8d9F9UyvNgXo1rLLem1uAzJHI0pt+ecHHPx29hqf0m+UO80bUpbKGyjPCF4WdjxHiXOcDljOMVI0q5t/wDSdrAgfOHUTnI/3Y22P1se+h/5T9M6rUbDU0BJmjMEngy7j7CfdVxbUbQ2lySPdD6YaldTTXF3M0iFtk4uEACryPpddXUkk8MfAqKFUA7Nk49uKzywMWnWDy3CvJJO2YYw3DkDmxPdnbxwas7PpDJCApgUMxAQLuOe2xqYuQNrRrUeqQLLFbS3K/OmC5Qdme/xqY90oOOe+AVPb3Vkkepi1tHuhITevIztJz4ewY9591WWl6tLPOEmB+Yp6c0jsFZgN+zmfAVspmbXdGhTaZp2oMlxPZp1oGFkxwtjzG9VF90XkA62wn48f7uU/Bh9/voTHT+dnkmijL3dy4jtYfzYkzjJHeaMIukMaI1spV7iJPpP0eLGSKVxlsfFopZkjmgfTNThlhLEMmRgq45Mp5H/ADqNcWs2kupkIeHIBcct+R8j8cjzLV1CHUdOWSe2EkMhxwOlRrrSy1i6RB7iykUgxNu6g8+E9vf35HbRxQinWGy1dYobn8pExaGUHdCefsO2RSupXTCzSkmHBIYDJBH5px39h7fCg2zvp7fUpIBJxdQ5RiO3hP37VetqjancLbIfooVBlIPNzyHsB97eFa4MP5ciiTOfGNkWewk10NPI/pNniXOygcgPAD76COkvyf6VA7SQQyvK3/D4VQnvJO/u51oU99BpsHAQI2I4vSOAR30Iax0mtZFNv86j4SMZLbY7hXvOMap6R56bbszG80SSzcoYmCjbJpm3Rlhe3xkDLKD9o+/30QzXMSqyLcxy4O3pjeqe4kUSqVCqew55muZxS0aIpby0VskMV8GGftqrmh6rHpZJ8KJybZ4nnKdaOQXi2z3UPXiP1zNLgOd+EDkPu8qxmjWDeiERSadK4XJ50nGa55Y77NrEV1TdLSwbU7ddTknjsS465oFDOF8AaiMuGIByAdj31k4tdDE1oPQ7WrpNCNhaWfzi4ikZ1whbCHG5HLnnnQCsbt6qMfIZos0LpS2lw28PUxEplCWj9Ig9mzZ94qJ4fyRcW6Jl2g6sF1NtTt5tUKlRmT5uCMejjAIGwySPtqc88dnqMWo3FqtxPNPxLxYzJIxyM534c9g2wMU9pUc2vZbTYHMrRr9I68UcYz2kHcjc4OM8u+iS8jh0qznSTTZW48cFxDwyTcQ7WG+3bgbVyLF+P2tVRrg9M8q9oCahDdy61cXlybm6l69l4RlkaAeiVUDltxHOKoY5WWS3FzJwwQS7uoyZAOQHeTt78mj+8h6/TgF+dWcFw3HdSS2zcUw5rErA+ipO7drYAzigttJm+byvNEuUkWUcbcOFBOcHu2x7qxy/JMiWCcHTQPdL5m/Ck8SFYkxuOIs7eZ+4fbVu1xc2y2GqcZazaOPrVXb0WUA5HaQdwefZVH0rGOk00ioRxKpG/eKJ9KiS96MW8Dn0WiMZPcQSM10yftQ5rroe1DSzPKt5ZyiK7XcOPVkHj7O3309aXTzfRzxGC5HrJ2HxU9oqH0bnl+ZyWNz+WtXKYP6OeXsz7iKtnQSKVbcEYzyI8u6s39MlfZ1RNQP0cfmamYwBuT51C1HZI/bUlFZIaju1PSGormgobc0wxpbtUZ5AOdIB1W50vNQxdRIcMwBPjTguEY+iQfI06Ywsewsbm205Wt4GtLFg1zGQcrEXGcEc/wA7Y8yc86c1M6Raa7JJp0LyafNEvCOIl1YAcXn37Yoe1rig0+x1PBLxXI48DmpHL7PtqPptx6c0MRLQo5Mb9uAcD7CPdWmRtYrM59MMV0qW5hEscqyW1w2IZmf0Hf8AQL/mScsB8Z+001yJY+simDCSM4YOMMPMdh7/APOptney2lyBbkLFfR8MqMA0bnG6sp2Izv4dlWV/Eus6XHcwxt85jHVFhv2bxOTvnA4kJ5jI5qa54pNvjtdk/oBp5Cjh1PpKcitX6AWhl0E3Wn3L21x174b10ZdiEkQ+sBnGRggcjWSXPokg8xWmfJBeM1rqNsc8KOki+BOQfgK2Krs0vR9a/GnSeP5tdLwrcw5zwN+awP5yMOTeGDvkUSWiEXN08RKpOVl5fnY4T+ytCuqaVJqdus1o6R6jAp6hn2WQHcxP+q2PYcMNxUzo10iS+hiU8Ucg4o3jk2dGGxVh3ggg/wCdaRdFBV82OcmRyfrGvJbSF1w6jPf207HKGXY04B25NbKmhdmX9N7efQdW0vXoIuI28jRkrsHVhgqT2Zq01n5l0gsdOu24ZbFiZU4zgBiTkHuIyQQaNrtLeW2eG5iWWKQcLRsvEH8MdtCk/Ry406G4Gj2jPayv1j2M8wADci0bb8J8DsfCocGtFJ3sz/pLpskF8LgDigZFVZF3VeHbG2w2qqtlSOTr5mAwMIO3zqX0gW70+4d5dL1CEA7DqSV9pXINC8nSCKRyZ41VxzaRSufOsrbK4pdhhZ3cSuZWyIUGMDmxPZvtT4vyCZAIoIFHqgbY8aCJNfSaFI45ogFbIVWHb4UiXWDJEoWKWZScklTwnw8ql2WkmE+jSJFK12sYWWVuC3yfyak7kfAGiW1iuIOrgVzAOLjmmZclj3DvoG0u7laQ3dwrCKEcbcW2ccgB51afhNryTrJpSzcwS2Avl3VSQpyo0601IX6vbxIUghHVRjGCcLkk+dElpNDNZxtC/okAgHb/ALVl2m39xFZcPXN85dhNxYB4RyUe6iC41C7Wyghs4epIHpyHAXfuwfsrWM/szkmWms6DpGpTG4WSO11B9hJjHWHsDj87z5+NZprOvQ/JpaxWGpW80+pShpesVMRzMTuyt2jJ5cxRJqb3SaradZK0hRFk4nI2GP8AvV7qmkaf006PS6fqBK5BMFwF9OB8Y41Pt9o2rbB6l45OicmHlFHzV0k6e6j0hmRp2EUSZ4EjB2z3mhiW9aTfJY95qz6R9GtQ6I69c6RqkQEibo49WVOx1Pcfs5VD0jT7i/v0W2QkhsjHfXdzlLsw4xiRIlnuZVjhjZ3Y4CqMkmiWD5PelUvCXslt+L1etnVSfIZz9laR0Z6J2PRyxfU75olaNeJpJWCgHzPKrjRSL4yatc54Z/ySsCC0Y5HB9VO5eZzxNkkAarDdW+yfyfSMyt/k+6S6fbyyMlq8JUkhLgZBxzG2M0HXpUTsi7KnoAHY7cyfM19JXOrxRDhLjlsB5Z+G/ludqF9XvrK6m6preOZ8lWLRhsEcwBtxMO3cKv5xB9GqnijFUmKM3d0YSxycDJxXohlYZWJyPBTWwDT7IzyR9VHxwjimRCAtuO+WQgKp/VAzSp10m3W26wKWu2At0weKYfpKp34f1jjPZWLxf2X+T+jGjlTggg9xrzioo6T3Gn3Fy8dtEoCMV4lbi3B3xQsRgkVzz5RNIuxSyMjZViD3g4rWPkTsLbW9Y1aPVrSC/to7QcK3UYkCOW2IzyOA1ZJWp/J/0t0Don0P1Iy3p/C1yWPUrCxOAOFADjH5zNzrJzbRSSs0jSpLaxsIrazhht4QMlYUCgk8ztzry/Ly3CtDbLPFzJRyr57dsjPvoX0rWYry1jltZRJDgBW5HyI7D4VeR37hVPEAew9ntrzWpX2e9jlGvboc1P0lEQjlOHAOJBJgd+apOlUazWqOw4eHTlLMVxuCCFx343zuKuHa3nJe4iljLD0urduBv7NC/TfU4NO4cWUDNNGURRmJsEYz48+R7aFFt0jm9VC/fYHdLZi+rKYmVB1KNkcznNXnRaVZdDQLySV1+B++g7U7t7gxSNAwMCKjvxZVxvw7d/7qKOh8wksLkdolBx5r/lW0lUTzpLolX0bWOu2N/H+SnkFvOPEjCt/HcKuTsTVX0hz+BJnX1o3jkHhhxVm/rt51D0Zo8JqDqR2i9tTSagamc9UPOpGVUpqLIakSmojmgoYkNQ5m28qkzM3ZUGZZWB2NCQyoumLTk15GXzsSPbTsttKXyRXLE681Nddqia7Dt7d9R0K/s8EmOJnXxZWBx7gffQlpc5i1KJVY8Eno48x/2o80k9TdX8fErK8pQ53JyTn796ALmL8G6oEdeL5vMQQe0Bsj3isIrlFxFmWmGkhzpsbjOYzxAjs3P3GpOla1Npl+LiNeOKYdXcQE7SpnOPMEZB7D7aiW4zaPGwI9IjB8QKiqMGPvzv7P4Fcyk4VL+iF4LDpfpEUYXV9ObrLC5HFkD1CT292+x7jV/wDJFKQb9B24PuI/fQNLqdzCj2vXv80aRmeEH0Wzsfsox+SYNHq+pQk5VEXB7wSMH3AV02pLkUjZ4TyNVOs6Q63n4VsGCSyFRcLyBYDhWTzxhW7xg813tIzipICyRtG4yjDBHhQWVujdKMnqLrMcy7EGiy31CORfWFBGqaCLqMTJlZ1yCw55Bxn286o01bUNHfq7kkJ2Sc19vdQpUFGuROrkyZBY/YKeyKAdO6To0aB24dvWzkH21eQ65G2AJAfbWqyMVF5Paw3ClZEB8xVJc9FdNkfiNtGzMcAEVOj1RWXO3vr1b0NKzZGwAHx/dTbT8B2Qh0K6PMuJ9Isp+/rYFb4impfk96Iy8+j9ih744+A/3cVdx3IbtpU15DBEWkljTb89gBTTiLsEL75N+iqwSDhuLONxg9XcMR7mzQJqXyfyWD9fo2qLqkCEk27gLNsezsfy2J8aMb6//CV27vOFtk3JUkgiuiewli6uBQGzs2eXjWMsi1RSQGWPXIOsmzFnmXPpe7nmrq1uhqEMQnyQoAA4sbCg3XtTlsOleo2aWl7cFJyytGgIIYBuZPjT0F1rc8RXT9FvSz7ekUXh+2okm9Gqa8hJqurJcXEvU5CRpwYTt78Hz+FF1jqsOn6JbLOQzFAJcLw8Lcyu3M+ys2h0TpqQDb9H0T+lukXFXVhofSnrovwtoxNsm3DaXi8W5yTkjf2Yqoxd9inJV0Sum+maB026NNYyyyRanFxS2t08ZIjON1YjkhAwe7nzr550meXT714QyhkYqSpDDIPMHtHjX1pF0d6N31ksF3osbxdq3IMgz45JpB+TDoO+T/o1p+++Vjx8DXdhycDnnHkj5wuLy41HqVu5pJ4ojlI3YlR7OVXba3MUCmRiMcia29/ko6EvnGhRIT/w5pE+DVDl+R3oi4PVw3sPjHeP95NdK9UkZfiMRl1admLiVw5/O4jkb527t8e4dwxETUJIlIjmMI4MGUE5jRe0eWdh3nvOa1+/+QzTJsmx16/tz2CZI5R8FP20Faz8inSqzSSSyvLDU4kHF1SkxSyY3wFORnt570/zwYvxyBqzvFNtatc2vXWiS/i2nscRk5HpOB6xGRz9ZmGdgaGtc1eZ9Vu53uOv1KUlJrhT6EQ5dXF4Dlxe7bc3d5Z3mlxtbam9tpOoohytyshuFjIzxIq5U5ywB2PPehQ2IWPrMMsR9JS/rMOw+2k3yf8AQ10uyvfIwPCmm507KcuTV3oXR0azaST8ZBjk4CB5Z/fWeV1E0iDtdRpcdA2EDSQ3LKVBPC6Zz4Ajt8KDORxXMmnoomWOp3mmyGS0uHiY+sByPmDsaK7b5S7+G3EcljbSyY9JyzDi8wDigiuFU4xlsuOSUfizZdG1+fU9FtrtkSKR+LiEWQMhiPhiqTpfGLyG2nlbJjlIzjLHI7/Z9td0W9Ho1aZ7S5/vH91SdXXrNLmHavC4z4Ed9cjSU+g5yk+2AFzOVg4WMgbHASRzGc4NFXQuQEXaZy2EYn3j76Gbu1Ly3QJJbg6xSVAzjny8DV10NuVF68WOHjhO3fgg/vq5/Eb8hhfW/wA70+4twd5Iyo8+z7adLcu/G9dmkk71zkHuar9TO8Xkamk1B1IgiP20AVMrVDkbFSZTjJNQZpABQUV13NMkoKOQO0CkR3sw9bhYeIr2dgQT40mPFaKqAkLcI3rQg+TYp5Tbnmkq/bTSgHsFPJGndSHYW6QjP0m1BhwmJSww5I5jcjxoV6V2+NTWcDAmUZ8Svon7qMNIIuOkE6RERiSRSeKQDi2GfPlVN0nt1ewt2PrK4bP1lyfupRlTDIrgNaTIzaTHxnJHo5PhXFj85AzgAk/ZSdKBXTB9dvupEjlbhznlGf3ffWeRWZLRW3LZJJPPetB+Sp+K7uZCMERLGT34bb7PhWd3Boy+TmdrXV7VfzZkZXH1mwp/tKB7a1S8DN0jNSVbFRIMlQakimWSY8szK26ncffUa+0iK5Q5QEHmMU/G29S43yMGigM8vuictvKZbGR4mzkqDsfZyNVrzXmnvw3cEi4/3kW3vFas9ur9lQ7rSo50IZFIPYRRQWANt0gZgAl0vlL6J9/L7as4dXvUHFwhlO+VORUm86GW0xLIhRu8VSTdDL62kLWszA+BxR2h2gpsOkB41SZGTO2TyqLrF587lRQ2VBzih46X0igGx4wOxhmnI7qa14jeWa8Qx6hKn40nIEiVrl+bOxjjjA4mPCzd2eWapLLUhDKqK7NJyCqvEx8gN6j6rdNrF5a2lojQwiTHEw3J7/Hvyedax0T0e20jS16q2CyP6z4BY+Z5mpjHlIbdA3pWhy6jdPfXek3fWSEbygRg4AAJBOfso3tNLht4gvAqfqpyqTNdxW8ZeXiVQMn0SaHbrpbDxYgdSv1Tn4V0VCCItsJljSMeioFNS3ttD68qjwG9Bc3SeaTIAf3f51Vz6jLOd2ce6peb6HxDK812wTOBlsc8YqmbpY0IKxrxL2d4ocOHOcuT4kV4Ih3GsnOTKou5ul98wPAFX2VBl1/VZv8AzLKPAVE6sY5VwjH6I91K2wo8e/1Bz6V3N/bpl7i5O5uZc/XNPGMDsHupDL6NHYGd9MOkNtZ6pJFqWnxanKYYzbCccj6QIJG5XltQDq161w5EswkmZg0pQBVU49VQOQAAFEHypp1Wu2Uq7EwEZ8mP76BS+VCjOB8a9XBO4JHPKPZ454mJo9+TFutm1K1JODGkoHiCR/ioAox+TK5EPS9ITyuYJI/aBxD9mlnVwZUdmoPbxrGTwA7YIO+RWEavEsOs3sa+qs7ge+voS5UCNiMcqwDpBw/6QX/Ccjr2x764sPkuRW16K8rhzroRJpHRwkdHLLyf9s1Mu5AlnKWBIK4wBnJOw+NQNCYJ0fsRn8wn+8adur22t5YRcXEcQBL4ZtzjYbe37K5ZdyYIGr/rI9UilnYtFxbDhAyp559/bTPRWYRdILdSNmLIPaDSNRuLdn4YuCQHPC/GcY5DbFVun3PzTUIJj6qSqzeQNaJXE0kzWeKvC1RY761mP0NzC/dwyA/fT2fCueqIF5qFqR/Je2pXFUDUm2j9tICquHUeswG/bTIRJOTKfM0m7HHkZ8aipCezHwppdFEl7MuPyJb6oz8KaNkg9ZGXzGKeiEi4wW9jVPjnuQPykntXPwp0MqhaL+a9OLbOvIg1afOWb8olu/1kwfhSg8J52a/+2/8AnRQFxYySL0h4TxTGeZchRgqD3d1QNXiM8KQjcsOEZ7+Db7RUuBmi16Mq3D1iqCc7YHaa9vJE+cHCAmNlIJUg5Xtx3VHk0fcQc0qQtpxGeTnbzApE5w5PeuPtpy0QQLcx5wwlJ4cchyFMTnc+VEjmWivnNEvQqfh18Jn1ba3Ht65G++he4Oxq76HScfS5VXk6hfYrIf8ACa0j9j8n0XatmMVMFVenyZjWrRTTKHFO9SY25VFFOo1AyejU6pBqEjeNSFagCQEU1xt1PZSVfFOq9MQ1JbLwEYob1bSo5pYFx68uPPYn7qLGYcJyKpro9brGnxKMAGVz7EI/xUmNATZaLnpbZw4yFZnPsU1qG0UQUDGBQ1pkKnpTJIB6quAfcKv7iUZxSj0DKPXp2Nsy7kHxoYEXFvir/WXJXAxVTGCVFTLZSI/Ub17838KmBK9KbVIyCIjxYx40rqtztUsqMZpJxQAx1W1J4AKVLdQxHhaVQe7OTUZ7xfzVZvZj40CHGUUy4HCaaa4lfkgUeJzUeaSYKfSHlinYGX/K1COu06cc/TQ/YazYHNaH8pb3M4gLherjY7jPbWdiu7DKkjJiquOidybTpZpUwOMXKKfJjwn41T1O0YZ1zTx33MX7Yrol3FiNt1hZhbSBZmUgdlYTfqy384ZizdYck9u9b1rBzDN7awrV14dUn+tmuHEVIhV1dXVsINOjU/HowTP5KRl9hwfvNX0un217YxGe3ilxnHGu437+dUPQRbOaO/iu3deHgdOHPiDy9lFcvUwjgt2ZogfRJ5ms0qkwBifo9p+TwwvH9SQ7e/NV0nRu1yeCaYeeD+6imRgWNRm4SeVUwBz/AEdjBBNy+R/Nj99T7C2fTpOOO6uX39QuAh8xvVnwg0lggO+wzSbsC0LY7RUDUmB6vtODyqWZrNmPDMvhkkVHuIIZ8YkU47nFc7RSKOZvW8qbRqufweME9W5HgM02bSEesCPM0hkWI5xU+PlSUtIwRwn7akLBgcxVAeCuMcbc0U+yliJgDyrzgYDcGgRYWnE2sIqLmRkHYMjfnvTV1tNNGM8fWOCDggbncGvLeSO31KKWbhJAABLgk78/Gmb0jr5wMsOJ+znuay8mt+1FQ0oj1G7gKgseLB7iHz8MimZo2MLS49DiCZz24J+Fe3m+vyy5wSvI9uSP3iuldvmrpn0eMNjxwRTrRikVUy5q36G/QdJLaQ82LRj+ySfgPfVVIdzUixvUs9Ssps+jEwZyO88/swPZWiEfQ+kyhol3q9Q7UBaNrERRCJAVYZBzsaMbS9jmAwwJoRRYA0tTvTSnNLBoAko21PK1RVNPKaYEpWzTqneoymn0NIB52xGTVHJdx22srcSn0IreTA7WYlcADt5VdSDijOTio+mRxi5uHwGkUgBiNwMdlMYJ2+oavb6zFNb9HNVmtvSWWbq1j9b84KzAkA9mM4qeOkdpcTPFHdWzTIcPF1yh1PcVJBHuozBqo1jo1oGuKfwrpNndn9OWIFh5NzHvp8VXTFYO3Usk6YELkntAzio0s9vYRZuZo4vB23PkOZ9gqJqvQnopYsg03SI4Ze08RYY8iTUSHTIYGxDAieKrg1jLplofOuwMT1VrdyD9IxiMH+0QfspLapdSbR2kaeMkpb7AB8afSzUbsMmnRGijZRU9jK/rb6Q+lccI7oowv2nJr0WzyflGd/ruTVjwjHIUgCgCKtqqDu8tq96pR2U+1Nk0xDTADkKhz+qaluedQ5z6JpgZz07gEtjIcbgZrKK2PpQFlidCdiMVkd5CYLll7DuK6sb6ozY0DTttOba7hnX1onVx7DmmBXtb3aEb5q79Yj9WpPGMqACef/esl6T6PLYMLqZGUzuQuSOwb7e0UZaPJ+FdFtrtpAjMnBJwZLcS7HJJI7jy7arul2mQjQJLlWnd4nUjjlZhucHY7dormj7XQ32Z3XV1dWwgp6DTtHqtxEGQB4D66gjZgaL7vj4uISLnHJVHDQF0Tw3SK3jLMokDrlTg+qf3UdXadU3ACxGM+k2an+QFfI8oJyoPkaYMpz6pHnTkr1HL70MBzrWPZXq8U0qxjbiOM86Y46esGB1CEEgbk7nwNSwHptMlTdZImH1CPgaiPbzrvwD+q/76vZmQjHGnnxVXTSKoJLbd9QxkKOWeM+i0ikd29TYtSu1XBnyO5wah9YpfAYE9wNTITkCpGiQl+zbtDbyeQXNSUuoCPTsyPFcj76ilUYbqD5ilJFH2Lj6pxQMnrJp7nB62P2g/EVJS1sJPUv8Ah/pIz9xNQEiO2JZB4E5+NOi3c/nRn60f7qKAGOi9zNLZpK0cTrakoDJvkesMduRy9oFWtzKzTyu2OPiYnbbO9VfRS6lCy2Toh6jhkhdlGAhbLZ7x2juyauri0kjlJcrxzuQiDJ2JySccuz31GRe5lruKKXVVK6vC7qFaSItgfVUj4VGlbCkd5q81iyiOqWLuzlWl6k5ONurP3imnitIRkKhbHYMk066Rm12Dpjd/URm8hmvPmNw25VV+sauZbhTsiMfPYVHLyudgoHlmqSFRQxavqWk3UiWt5JGFc5UHK58jtRdoPyh6qpb5wImCY3XKk/d9lAM7cc8jk5LMTn21a6eix2gJDFnOdhW0kqBM2LS/lVtdkuusi8XXK+8Uaad0usdQQNBNHKD2xuG+FfOLcRGyBfOmgzxOHWVkccihwfsrPiFn1hBqNvMBwyDPdmp0cgbGDtXy1Y9Ntd00qEvWmUfm3A4/t5/bRZpfyzm3Krf2jjvaB+Mf2Tj40cWOz6BU7U8hrMtI+VjQL8hfwlDG524Z8xH+9t9tG1jrdvcoHV1aM7h1IIPtFTTQF3M2Iaj6QwJvHPbIB7l/zpuW5jlUKjgmlaapt4boMdzN/hFA2WZnqJdXBCnekmYZ51EuHDA0mBSXLmW6Zj5UyVANLf8ALNivDWTKEGvK9NNs1IBR5UjNNT3KQxNJI6og5sxwB5k0Kan8ovRzTQQdRW4kH5lsOsPvG321Si3oLCxmFR3mAOO2sl1T5YJ3yml6cqDskuW4j/ZG32mgzUemGvatkXWozdWf93EerX3LitVhfklyNv1XpTpOmOUur6JZP+Gp4m9wzQrffKHaSMUtoZSp/PfC+4c6yRZX3wcZ547aWkhBBzVfjSJc2afBrGl3rhpw4bvm9UewVQ9P7O1a0sb+1uIpMEwssYxgesNvfQxHcyKchjTlzcPPZyRsxbYHyIqoumTZT11dXVqM0v5JrlLqW/0iRA7lRcwjYbj0XGT4EH2VbfKjK2j6FBZiGLN+xBPMqqcJO/eSR7jWbdFdabo90n0/UxusMo6wfpIdmHuJo3+WDW7HVX0iK0lLtEsrOMcgxUD9k1LXdgZhXV1dVAXPRORIulmlGT1Dcop8icffWv6x0ce5IaEtbso4TxrkN7By9/srL+hNvob65C2vz3VtDxK0M0LAKrg7cexIXxHKvo6W36z0iq4bcHnkHfI8Khvvobi1sxW70HVIScQJKO+OQfA4NVctrfRH07G6X/2SfhW13WmwFSzgADmx7KqpNLLfkCwH6TbD2DmaXIVGQuZlGfm8/wD8LfupVoZ/nKs0DqoByXUj41p8mmTqdzxHvNRWspmYqF4j3dnvqWx0CMbxtjrFwe+n+ojlH0KiQ9rclHt/dRL+B2kP06o/6vAOH/P20+LK3gITqA0mNlCb/wCQ86imUCB0KO4b6ZesPYAMAeynItAixiCMkZ58R4R+/wBlGcVkjbyogH/DTl7TzPw8KmJawHA4AByGKdMQDvokoHoXDhu0lQR7qa/BmoxnZoZB5FT8TWgLp8Rb0kwvcOdRLu5sbORUW3kmHJjE2SpPLO2CPI9vZimkwA1YtQjYhrJyByZHBz7KdW6KFhJDOnDzJiJA9ozRNFqWlXkrpHOywIPSkVDue7bcewb+FTYG06aLMU8KoNgGITHsPL299FD7Mj0aOG6ni+bSkTwOQhQn04z6wyBnbORnxotmheTpBFA8sLlFB41zwjiJPaM7YoP1W7tbDTtO0bRT191bzGeW7iXeR8cl7So+6tG063udf6HPrtzEw1SFeBrmFQoZQuAjg7kjb0uYOeYGKJq+zRKuii1nQWVrJxf20wa9iQsQ4xxEjJyvLepMnQ/U2jzarZ3Z7Fhu1De5+E1m79J9Wkhjjku2bq3VxxKOakFTnmTkVe2/yhamksbdRC4C+mhB9I94OdvtquBlZK1PTdT0uYRahYTWTt6onjI4vInY+yqq6Yx2srtIxwp2zWsdDem1l0im/Al9aq0U5CfNJT1qSjBLHGPQIxz7Nt6yDpZLbwavqFnp7cdgl1IkEjElmRWIBoUQYOohd1QcycCr9pYrdFjLqoUYA7fdVJbRdZJnsWpEiiMdgq5fQiTLfoM8Ku3idqhyXsjerwr5Co7vxHakUJCFNI7nLMT5mk11dVAdUyw1XUNLlEthez2zg5zFIV+HOoddQBomkfLFr9gFW8igvlH5zAxufau32UeaX8uej3CdVfQXVmzHiZyokXOAOa79ndXz/XVLgmOz600vpno+rkCx1O0uGIzwJKA39k4P2VdG6DjfI8xivjHJq40/pTr+luj2Wr3sQTkomYr/AGTt9lQ8f0Oz6nLAyv4GkTyxW8JmmkSKJeckjBVHtO1fP1x8rvSua36uOe1gc85YrZQ59+QPYBQlqWs6lrE3Xalf3F0+cgzSFseQOw9lQsL8sfI3nWPlR6MaW7Rx3T30q/m2icS/2zge7NA2q/LLqE4ZNM0+C2B/3kzda3u2A+2sxrq0WKKJ5MsdV17Vdbm63Ur6a4PYHb0R5KNhVdXV1aCOrq6uoAWtPIKjU6kmD++paJaJarT6JnbG1MwgscnepQkRfRzk91ZsCmdCkjKew4pNTNRdWuOFVUFR6RHaaiAFiAOZ5VqtFHKpZgqjJJwAO2p2rCcXEQuQRKIVBBOSMbfdT8GjscFn35kDspzUrGe4lErNlgoG/bip/Iro0eKSVlLXU81rMv5hPlTZRl5qR7Kq0Zj8NwUTgOMdh7RWidBflFvNCjXTrlTeadxbIcl4M8yh7R+qdu4isyp6GQq3Mg+FTKPlG0Jp+2R9UabqWj64vW2F/HeuvMHZ0/qHGPd7aemhAJ9Fi3cK+aLTVJYSn0hyvI8IJHkef20Vaf8AKTrOmMv4811CNuouU4lI8GzxD2Gosp4fpmwywgcxTBEakcQGOzbn5VC6LdK4+lemNdJai2dJOqkBcMAcA5HaRv249tEkNjF6w9Ju1icmmYNUVotDcZ5wp4euf/8APx8qdTTI1HCiADnjHPzqzeBYhsrM2MhFGSf47zSvmhdsy8v0By9vfSAqhpqv6iqR+ljb/OnE0pRvjfvq2bghiMkjhUUZLH+PsFU95fSXdsrRxzx2nGVdk4GMg7gOWO3n5iqSAitNaPJPaxzokijAlc+hvkE7bnHuJ2yKrLjTNYWd5rK9s58ANcSfNmR1cDAKurbY78kAdhq2N8Z7leru4epjOS8yGMqR2k7k+QJ7c9lPpZNPbr1bab1BPAXjlwTnnn6PnnvO/tqkqGD1rpV5cNJ870yW5U78USxyHwHqgjzyR30xdaOkCfj2g3FtFGWP0cp4GHYdx6Pb6uaJ5orDTJolluIk3wGhcxhsnuIIBHIbjtqVaG2Lyz208yE4VvpAWXHI4U4Pfyzv2VQGU6V0N0TQbyCW9mOp32WZ0hdo4VwAwA5F85A7N80RapqOpaj0bvbbT4yS8JhtbeAKFwx35YUkKcE57O05qpt+qQMeBXkuT+UORsdigbmfYO3nRlpsAt3UKRjg3UDZcbAD3H/OuD8jlJWdbgoxdGPwfJL0ivBEUhjt2IzJ85lUYPgFzRloPyKQxNC+r3wk4X4njtwyiQdxYnI8wBWlxvsO0nkO+p8WcZIxtXTzbOSgei6P6N0O0K9m02zSFlgd5JScyPgE4ZjuRty5V8zamsr3WGU8QQMc+O5NfTXTyUx9Eb1RnMwWIePEw+7NY3+DGd8kLk9y/eaafYmAVv13AVhiZiTuQKkrpWoXG5iIHjtWgQaUqjBUZ7M7mpiaew/3Z822qrEZpJod3GM8OfKoUtrND68bD2VsCacHGGA9gxSZuj1rKMFFBPZzP76dgY3XVpV90GR8skXD3E7fZQ7e9Dbq3yUBYDuFOwBeuqXc6dcWzEOhGPComKYHV1dXUAdUpL+4j0+WxVgIJXDuvCNyOW9RakSBeFHHaNxSKSGCMV5Xp515TJOrq6uoA6urq6gDq6lrGzDOMDvNLEXhnzosBmuqQIGbspxbNj2VPJAResfGOI4pcUxjI299SPmLeNefMH8aXKLCiPM4kmZx+cc10YB8D3inHs5lOApb2UgK0b8LAg+NVd6KjvsKNK4epfr8vJj0RnC57zUmQCRMBs92AAKrtLZZoOq4ssfzTyq9isZ5DxOh4f1dx/lXJJdnoRpqioNsCScduMd1d80U81FW09rKhLBCAByA2NexWplUMoyD4U07ObLj4O/BUjS4ZdjEPdUmPopazjI4lPgavINNkLABCW/RHP8Ay9tXNppEm3Hy7gfiatNmLBGLoDHcbQ37hvFdh7alRfJhfiRXju4JQDnDDnRxFprxMCpAx2Va2koVzEv0kg9YA4C+Z7PLn4VdsVkTQLDVNNtupuorGO3QZ4rdVjx5gAA+dEUFzckgJlE/TYbnyH3n3U5axRsVaZuNxuNsKp8B953qyS3jcjhIJNAjy2uzGuODY8ydyT4ntqUdSt4x6YyefCOeM49m+2Ttms5n6frb6zexMLZLKGUxq8mVJC7FhkjJzkEZ2xtTUd5b6jdRXUl/M6yeq6kQtw9gyCQR25B/fTSBBJd6hK4d31KykRsRFGZ4wSCdxzGc9+cHtArySSYRLDHbyGJSH66C4jZdufoneqyXUJXSOOS/uFAJVHdSS3YeIb8X8b4pcN7c8avO9wynJWaBIz1fLsyreGxPlVor9Fr+E7SeeO3Fq0UrD0GkyhcHmCSvCc74yc+FM2KaW7tB8wEfVN6PoIx4jnJyOEnzFP22r6hAAqdVcRAeiZvomIHLhEg4WB33DDyr0XVncyubu14JtmCHjB7c7oSPdTEe3WkSRgSxvG3WLxgpcOvH2kspIONhjGTTkYQ2ySyzCUIuGSSBZGHickEjOPtqIkNoLmSeOQxQerLGS22c75LAk79uasBZq3BLZ3CQgH0FadoiB2sCTwkHuoEBcNoUmVyyhicqAvFxHO/GTz7cBe6iKyuUnd2QEbg5Y7kHl/HKhS3KS3qSBxJKz8ORJ1jA45ZHojl6o3350SWYWNpOfEzklichvI9o515uNe47cnxL+BqnwknFVds2fuqxhbfzrqRyFF03Bms7S1G5aUyHPco/eaFIdJ4sAhm8Bt8KMdeR7i+hVSoVE5kEnc9g9lRorBSPTLSb8mO3uGBVklHFYRI/CMFv0UBY+3HL21NTTCw/JBR+uc/YP31fR2qqoUAAfogfcKlJa7DC++mANHR0OeLiPgPRH2fvrhpgj2UBR3Y50VC0Hb9m1d8zGNlA8qYgVFoUJ+jxnmTXj2EUgIdAfIYomezBzgZ8qjSaex9UBfHGaYAZf9F7W6RsovtFBOrdAFJZrdWB7wNq2I2DA75bzpPzYH0SOI9wGTQB853nRPUbYt9HxAd1VMthcwkh4WGPCvpuXRop88Uar7Mn93xqru+hlpOpwgJ/W3pgfOLRspwVIrmyMA91bNqXyfR5wEAJ5DtNZRq1mbS4GXiLNnijUktEQccLZA327Miixorq6rVNEuns45xG4WReIZHMVGewmj2aNvOi0Ih16AT2VLS0Pb7qkx2gx2Cpc0FFekDNz2FSEtsch7TVglqO6pCW2OYqHNsqivW1JOd895qQlmO0VYpBjsp5YcVDY6ICWgH5tPLajuqwjty3IVLjsidzSCiqS0BPKpCWAPMVbJaBeynRbnupjKoWKAerTNxokV2nCy4PYRzFECWhJ5VMisj3U1aDozubQtT09i8UTTx9jR+sPZU/TOlc2mtwvGHI24JU3FaJHZKE4nwq95qQ3RyPUk4J7SNoyccUkQZj5A8vM+6q6ey1klFAFddLdKu0yunywS53Ak4oz7CARStB1MzaxHEv0drMCH4c42GQc42OaMZ/kj0e7GYTc2p743yPcaXp/wAkk1jITDrLGLtDxdnjvijitoHmbVMsbTSwqr1fDwnfbtqebMwgF8DJwo7WPcB21aaXoj21ksMMvXcPK4kX0f6o5t57DzqyXSQhLZZpCMGRt2P7h4DanRiDyWU0w9NTGn6IPpHzI5eQ99SorAooVI+EDkAKuVs2TmQAO07Uzd6itnDx29u19JxlDDBIgfIGTgMRnu86KAjrEYFBkyAThRjJY9wHaaqZ9bNxMYkZraFCCS0ZYvnsdccSjIOftNP23z6+unnuormQABTCCoZR25THYRyJ33qbEOKCRZYUmuE3KNCqOBtzzue3lmqSGUE2kadPNJPBAZkuCCXt5yMsfWOFJwd/0d6gXHQrRrqy6prqS3dW4ka6txlCTsQYyAfPHmKKJrOzYJxaRft1x4pZLWAcMW+PSw2SRtyyeZrz8DxIp+ZXvDGyjhAVpQQO9Tg48cVdCpATN0M6TQSTS6VqzXChGxF15lJAGdlYDJ278iodv0k6Q6dYrNqekxXjKeHrbjigf6rjkDntHuo9t7e2sPo5RaiJm3ikkdcHG5GSRg7dlTZ4NPFpEl9OyxMfRVjG4z2YcDPPPd2UUGjPP9LrGe7KNY3FoWHDIXtxcRxtjkyo2WHLfGcHltV7p19Y6ndTW2l39peyqq5hido2fGNzGwUtjIO2TkeFWF9p2h3NwEhtg9yRwiJ3XrGG/JweMDs3BHYaVP0Lgu5Y5ryznaMjJWTLJtjyIOO2lRVsS8tx1MfzmCaLq9mAhk27jxDO3mcdnbTnz2wT6IySISPRYw8QTv3UEgduw50zp3R5dO024sYNSu4HfaNIJJIY25bEBzv5Y8qlGK4Fqiyy9YWYBi4iyhB5ZbgJH8eZQf6AtZGCCbqRC+fSSISY4iRzOB6g7P1jt31c2OIEEYcOykhnzksQcb+NDmmJFHcF4SJWXjYSlfR5HlndjvniOwxV1HNwmMZJPCDnvzvn215+P5HVl+ISW02eZzVnDKMgUOW1xyPKrWGbI2NdJykmeIzXTuADsAMnFSo7UD+MVGVSNydzTyyyKNhnzq0STEhCjAUDypxUHtqPHdHk+fhU6EhhttTQCRGeIYAx2knf3UoQbbkt508pU+oDJ9Xl7+VLVHPMhfBdz7z+6mIY6gAb4HdmvDbEj0U9rbD99TVjVTkAZ7zuffSmeOPAZgCeQ5k+wb0AVj6eG9clvAeiP48zTZsQq+ioCjwwBVriWT1UEY75Nz/ZH3mvGtEbHH9KQcjj5D2cqYFA0YweBS/ivL38qbMLk7tgdyfv/wC1ED23F7PsqAUjkz1IaYjYmP1R/WO3xoArkgVW9QAEgnbnXzB0s0nUbHpRqcd1bSo3zmRuWQQzEgjwINfVjWkxOHYqP0Ytve3P3YpaxiOPq1QKvaMc/wB9FgYXJ0t0e8CwWmj3ixxoqByqknAA5ZwOXjVZcNazElNOuuI9r4r6D+b2ynJhhDHujGT9m9JextphhrWEDvMYJ91LsZ81z2Ejbi3KDxppNPkJ3Q+6vo9+j2mSZ/FUye3FQ5eiFi59CNR7KhxHZg8emTHkhqQmlSnsrYZOhsRz1W/j2VEl6FP+kfupcR2Zimkt51Jj0sLzXNHr9EZ07T7qZPRidR20uIWCKWXD2YFOi37AKJx0dlHPJp1Oj7D800UwsF1tCxqVFp5JG1FEehtkYUknwro7brHMVnH84dThmBxEh7mfv8Bk+VOgspodNCqWbAAGSTsB51Lt7N58fNYgV/40gPCfqjm32DxNEFv0e43SS7br3U5VcYjQ+C9/icnyq6i04L+bToVg/aaKiuJGBeXGONuY8uweyrm3sQuNqsvmyQx9ZIyog2ye/u8T4UtbeabsaCPy+kb/APz8fKnQrIwRVfgCl5MeovMDvJ7B50+tn1hzN6Q7I/zB7Pzj5+4VMhtViQLGgVc5wO09/ifGnJmW2tpJzG7iNeIqgyT5eNUB5FbcR3FMXN1a28zwHJlVFkIIIBQtgkNggkcyPLsOapNS6STGZLRbWWCCQNxOynLqcjGOEjlucEHl5U1btZIpdYIiqIIVmjdchRyClfSXHIA7DG1OhCtRnupowjWUM1q7MWeKbKcIHIkE/aB5bVW5W5khtY3jmhc4WCfAwMdjMME+XCat5dOiuI2a3uRdxMxPVytiQE9gkAB7hyOKkreCytUiGhCGNMIRxhhy7TjJ8yKfQyi6lDZoG0+KN0bgXhuDg797hgO384V17YPeWzJFPJauhxlpVd85yMLJ6LLgdje3NS0ttKvY5EaO4toy3GFt2UAtnJBXcN/3pmSxveIW1rc28K7qqXFiWYADYYDK2O3kceNUmhE6G3kgaOQQ3MT8IAuLdlIkyBklSfszzpepNcS2ZliuhJGRkdZDgod8k5zt9m9QEjt7KYrEZ+t5Spbh1QnvG2O/GcHlTr/PJYxC00M5kJAEkixsy5OxIyDkeGckcqAKyHVJZHi6toepVzFKqSKT6PaVZSN/DAqxLWkM4kijhmRxyi4kAbn6WTw+0e6lRxOZVF3ZNKI1PD18mWUctmIJ5DHt8q6KCJZg41sww8RC5jHPG44vdsSaB9jN1JYGRJGt4IiQdruPiCk88SKCRnxNMuI7d4YPnR+cz5EZsJGOAowc8PpADI3JxuO3FWstvNwgtcxzqASskYVfeMc9z2/HbotGSS3Eyw9c5GevWPiJzjngg9gzjNAFdCb4XKcGoRoq5WZL2AEkYwArYGDkduQfdTqWd4VeV9OhlVhzjAZZOWxG495qOTexSqsdwYVQ4KPIwD/V6zIOBjK4BpwS30Vsz/g8KOfWWYaNmOAfzcr7xQCbRn9pHLBI0heQMITGjuMuwOANuwYOQvaSOzNeLehjxkr7DtzPKk6dPHqEMxiaLqyGOYeQPgx3Pn2DaqLUryaS6mSJkjXPArEZJwMZ7uyvOx/Kjry/EuH6V2NpP1ck/CFPpEAnHuq0fX5HtAsGFnkGwVuLq1PIsf0sdg5GsdvQtrehmuhMSct6JO4+yiLQOkrS6ottPA4ikcLE/B6vZgjzrp4s5jXOjmsYhW1uGyU2VicnFFSyRvsrZJ7F3NZskckc+QeR38qNdAnd1CEej3U0xFr1TvleFQDsS2/2VNt7VQFBHFwjAB5D2cqcVYkYBmzJz4FHE3uG9So0lYYRUhH6Tjib3DYe0nyqkIdCkLlsADtPIUlZ1kz1KmXHaNl/tHb3ZpS2seQ0nFM4/OlPFjyHIewVI9YjO9MCGxbrY45pShlyFSFTjYZOXxt9makRxxxAhEC55kcz5ntpEl5BFIYgzSTbZiiXjceYHL24pHBez5yyWkf6mJJD7T6K+5qAHpp4bZBJPKkSHYFzjJ8O/wBlNC4uLja3tyi9ktyCoPknrH28NKhs4LeQyohaY85pGLyH+sdx5DAp4s35oBOe04oAYFishDXMj3Lfovsg8kG3vyakGPbwHLwpPXqchPTIOMLv7zyFKw8meNuEfopt7z+7FAhqRUB4SMt3AZNMvCXHIIPDcn28hU0KqrhQAO4U2wzQMrjaqpJUYJ5nmT7abMbCrBlzy3+FIaIN62/woArjIcegvEe/OB7/AN1eCPiOZWL7+ryUezt9tTXhyaZaAjlQB5muJIruBgK9waAPNj3Ukop5qKcA8KZvL2006JZLuYRhzhFwS8h7kUbsfACgR783Q/mD3VDup7S2nFssTXF4RkW0ABfHex5IPFiPDNLWLU9T9cyaXaH81SDcv5kZWIeAy3iKsrPTraxh6m1gSKMtxMF5s3exO7HxOTQBTDSJr3fUGURH/wApAxEf9dti/lsvgas4rCONFRECqowqqMADwHZVgsPhXsskVsyo+WlfdIkGXbyHd4nA8aKAYSyGcAV4PTJS0RZSNjI35NfaPWPgPaRT4t5rne6IWM8reM7f12/O8hgedS1QAAAAADAAGABQBDisVRxI7GWYf7xhy8FHJR5e0mpKwZ5Ut3jjwGYAnYU1NHcTKOFlEe2VOx2PPNAxicsyskIVz+b1ZGcdpz393lTHouwSQvgHlKeE7cvSGx9tPC1ktnPVxqQw5H0d/fv51JUOI8NGU3xwlgRRQyEI4yI1kV3CjIZvSYdnP+OdQpdFtriJZEi9JzksmzKfs+09vOrc28DkYYKTuFRuHiPkaZksnJbgdo3zniC7k+H+VArB06LLFcccV60i8W68eGBxnGSCfZ51IN9fxQHrC7IueHr4CVJ7RxLgrjvNWsi3kZUyxiYbqWX1vYQfjmkq0bnEgli9HLcaDGO3cbdvd20WOn4B7rLR3aeU3NnN2kKtxEfHYBjjxzTryXQV4utM6huL6J+NO/dCDj3DlVnJbzCTrhHb3cb79YE4GP8AXTnyG5FIn43ys9oxjBGGdRLgDl6Q37O8c6oRUxT3PG0fVSOowccBfh5DluRjvG2xp6W+lA4jp1s8behljxgHxxnG+Pcas7S8SKWWWR3mznheJuNU22xnBHLcZ7fbSZ4FuVIf5rdBh6PWExyEDtBOG9xPOgCpDQXSI8lvJDCzYVWPHGT3Dt7RttXiaNZXt7l7ZopQfo3kRZFYdhU+/tPKpc0AtpAHedBj8jcR9bk+ZwSOfInnXkdtZTIC0csM/CQGjLFA2+DscgbnbGaYiFcWl5azmWWeSUnZZImJ5jbIPLt5CmoNV6rrLS7ublATnqVQow4jnIAXc89lIqa41GzhB6qJw/59vNgNvyw2/aeYqO98S/BNbzRufzmUrzHMMDge3u5U7AZa+KozQpc9SZOJ5DGFycD0mALf3hz8qnpKXsALa4aGbKvGxIwW/q7Ec+zbblSfm0N3cieG7lgVYwjR8IXOcnLN2nfcjOcnIqJdTw6ZKoa4uXJAZ1S3Lxb4ABAGMjmeXf30rGZneO+l6XOY345AixlmAAPogjAGAADvgc+3NAq6dPdkM15hmGc9XnHlvXV1cWHVnRmJ1l0VtC6rNNPLvjd8D7KMNC6O2FjKGijHHnIcgcQ9tdXVpybMaCUW0YLSHJC42FFOl2aCNCWbDAHhQ8I9vaffXV1WhBFbqsScKKqrnkowDU1Bkc66uqxDGoXg07TZrwx9Z1QHocXDnJxzpMUEl9axXFzcP1cq8QghzGuO5iDxH3geFdXUATI4Y4YxHEixoPzUGBXm/fXV1ADVxL1EDy8PFwjOM4pPAZFQyMSCM8I2H+ftrq6gBwHAAGw7AKWPOurqAOLbZxXAcXP3V1dQBxpBFdXUAcVGK8KDFdXUAJ6tTXnUqa6uoAo9Z1Ge31zS9Ds+GKXUQ5+dMvH1QXnhORJ7ycDuNWNlpFrZzNOA014w4Xu5sNK47s42HgMCurqALBYxTqoK6uoAjXVxINSg06AiNpo2kMxHEVA7ADtnxOfKpEFrFbhurU8T7u7HLOfEnc11dTEP4wM1HW4aSa4jA4RCV3HM5Ga6uoAWYxJPljv2GvUidRwNL6QOCUHCD7N66upgQ2uGguTbEKyFSQAMAfx50/b3BcKMEA9gNdXUls0roZ1CERGJnWKVS2AHjBI7t/A02LuZmkCtwlVbnuNv4766upvRlfZFj1K8huSJHikiLFcdXwsOfIg47O6rNpM26yyIrht+HGMcq6upLs0n0Qo7OMF2hzAzMc9VsCN/zTkZwMZpYu5IbpYWAdmdV49wdwP311dQ+hLt9jtxYQXW8sUfExALheFuQPrAg1A/B6mynkSVikacXVzASA45c/Ic811dVEFL1dxBYmeG7ZIVZQYcZHJTtnYDbljtpqe6tru2ggvbJJOuWHDRMYyCwTfG4zvzAHhjnXV1AyWCwtGgld54EIi4ZWLMeQzxHf8AOzU6z0grPcKbuR1t0GFZF3JLbg4yOXeRXV1MCPdxQara3DS20JNuyrll9IkjPECuCD76gQRcOrQaZxuOtQlXDZAAJ5q2cnbnt45xXV1IaP/Z";
const BOARD=[
  {i:"PT",n:"Per Thomsen",r:"Senior Advisor",b:"20 years in Nordic private banking. Former Managing Director at a leading Scandinavian investment bank. Specializes in cross-border wealth structuring."},
  {i:"HL",n:"Henrik Lindqvist",r:"Banking Relations",b:"25 years in Swiss private banking, heading the Nordic desk at a top-tier Geneva institution."},
  {i:"SD",n:"Dr. Sophie Duval",r:"Regulatory & Compliance",b:"Former senior examiner at the Luxembourg financial regulator (CSSF)."},
  {i:"AM",n:"Andreas MÃ¼ller",r:"Technology & Innovation",b:"Built and sold a European wealth-tech platform. Now leads Aureum's technology."},
];
const PORT_H=[{m:"Jan",v:2000,b:2000,rb:2000},{m:"Feb",v:2065,b:2025,rb:2095},{m:"Mar",v:1948,b:1910,rb:2020},{m:"Apr",v:1892,b:1858,rb:1975},{m:"May",v:1975,b:1935,rb:2055},{m:"Jun",v:2042,b:1998,rb:2125},{m:"Jul",v:2105,b:2058,rb:2195},{m:"Aug",v:2035,b:1992,rb:2148},{m:"Sep",v:1995,b:1955,rb:2110},{m:"Oct",v:2125,b:2078,rb:2225},{m:"Nov",v:2185,b:2135,rb:2295},{m:"Dec",v:2164,b:2120,rb:2360}];
const ALLOC=[{n:"Equities",v:42,c:"#4A8FD4"},{n:"Fixed Income",v:28,c:"#C9A96E"},{n:"Real Estate",v:12,c:"#5EA17A"},{n:"Private Equity",v:8,c:"#9B7CC4"},{n:"Alternatives",v:6,c:"#D4845A"},{n:"Cash",v:4,c:"#8B8B95"}];
const FEES=[{l:"Management fee (bank)",a:"\u20AC16,184",p:"0.70%"},{l:"Custody fee",a:"\u20AC2,312",p:"0.10%"},{l:"Transaction costs (est.)",a:"\u20AC3,468",p:"0.15%"},{l:"Underlying fund costs",a:"\u20AC4,624",p:"0.20%"},{l:"Aureum fee",a:"\u20AC2,312",p:"0.10%",au:true}];
const HOLDINGS=[
  {n:"Novo Nordisk",sec:"Healthcare",w:"6.2%",ytd:"+52.3%",cont:"+3.24%",val:"\u20AC143K",chg:"+2.1%"},
  {n:"ASML Holding",sec:"Technology",w:"5.8%",ytd:"+38.7%",cont:"+2.24%",val:"\u20AC134K",chg:"-0.8%"},
  {n:"iShares EUR Corp Bond",sec:"Fixed Income",w:"8.4%",ytd:"+4.8%",cont:"+0.40%",val:"\u20AC194K",chg:"+0.3%"},
  {n:"Vanguard Glb Real Estate",sec:"Real Estate",w:"5.1%",ytd:"+12.3%",cont:"+0.63%",val:"\u20AC118K",chg:"+1.1%"},
  {n:"Nestl\u00E9",sec:"Consumer Staples",w:"4.9%",ytd:"+8.2%",cont:"+0.40%",val:"\u20AC113K",chg:"+0.5%"},
  {n:"Swiss Re",sec:"Insurance",w:"4.3%",ytd:"+22.1%",cont:"+0.95%",val:"\u20AC99K",chg:"+1.4%"},
  {n:"Roche Holding",sec:"Healthcare",w:"3.8%",ytd:"-2.1%",cont:"-0.08%",val:"\u20AC88K",chg:"-1.2%"},
  {n:"Partners Group",sec:"Private Equity",w:"3.2%",ytd:"+18.5%",cont:"+0.59%",val:"\u20AC74K",chg:"+0.6%"},
  {n:"UBS ETF Gold",sec:"Commodities",w:"2.8%",ytd:"+14.2%",cont:"+0.40%",val:"\u20AC65K",chg:"+2.3%"},
  {n:"Cash & Equivalents",sec:"Cash",w:"4.0%",ytd:"+3.8%",cont:"+0.15%",val:"\u20AC92K",chg:"0.0%"},
];
const WINNERS=[{n:"Novo Nordisk",r:"+52.3%",c:"+\u20AC49K"},{n:"ASML Holding",r:"+38.7%",c:"+\u20AC37K"},{n:"Swiss Re",r:"+22.1%",c:"+\u20AC18K"}];
const LOSERS=[{n:"Roche Holding",r:"-2.1%",c:"-\u20AC2K"},{n:"Zurich Insurance",r:"-0.4%",c:"-\u20AC0.3K"},{n:"Swisscom",r:"-1.8%",c:"-\u20AC1K"}];
const CCY=[{c:"EUR",w:"52%",clr:"#4A8FD4"},{c:"USD",w:"24%",clr:"#C9A96E"},{c:"CHF",w:"12%",clr:"#5EA17A"},{c:"GBP",w:"7%",clr:"#9B7CC4"},{c:"Other",w:"5%",clr:"#8B8B95"}];

/* â•â•â• TRANSLATION HELPERS â•â•â• */
function translateSector(sec,lang){
  const sectors={
    "Healthcare":{fi:"Terveydenhuolto",sv:"HÃ¤lsovÃ¥rd",en:"Healthcare"},
    "Technology":{fi:"Teknologia",sv:"Teknologi",en:"Technology"},
    "Fixed Income":{fi:"Korkosijoitukset",sv:"RÃ¤nteplaceringar",en:"Fixed Income"},
    "Real Estate":{fi:"KiinteistÃ¶t",sv:"Fastigheter",en:"Real Estate"},
    "Consumer Staples":{fi:"PÃ¤ivittÃ¤istavarat",sv:"Dagligvaror",en:"Consumer Staples"},
    "Insurance":{fi:"Vakuutus",sv:"FÃ¶rsÃ¤kring",en:"Insurance"},
    "Private Equity":{fi:"PÃ¤Ã¤omasijoitukset",sv:"Private equity",en:"Private Equity"},
    "Commodities":{fi:"HyÃ¶dykkeet",sv:"RÃ¥varor",en:"Commodities"},
    "Cash":{fi:"KÃ¤teinen",sv:"Kontanter",en:"Cash"}
  };
  return sectors[sec]?sectors[sec][lang]||sec:sec;
}

function getAllocNames(lang){
  if(lang==="fi")return["Osakkeet","Korkosijoitukset","KiinteistÃ¶t","PÃ¤Ã¤omasijoitukset","Vaihtoehtoiset","KÃ¤teinen"];
  if(lang==="sv")return["Aktier","RÃ¤nteplaceringar","Fastigheter","Private equity","Alternativ","Kontanter"];
  return["Equities","Fixed Income","Real Estate","Private Equity","Alternatives","Cash"];
}

function getCcyOther(lang){
  if(lang==="fi")return"Muut";
  if(lang==="sv")return"Andra";
  return"Other";
}
const WA=[{f:"u",t:"What happened in markets today?",tm:"14:32"},{f:"b",t:"European stocks +0.8%, led by healthcare. Novo Nordisk +4.2% on strong earnings.\n\nYour Novo position (\u2248\u20AC143K) gained roughly \u20AC6K today. Euro steady at 1.0842.",tm:"14:32"},{f:"u",t:"How is my manager doing vs peers?",tm:"14:33"},{f:"b",t:"Your YTD: +8.2%\nPeer average: +11.2%\nBank's benchmark: +6.0%\nProper benchmark: +18.0%\n\nYou're beating bank's benchmark but trailing proper benchmark. Top 40% of peers. Fee (0.70%) slightly above peer avg (0.65%).",tm:"14:33"}];

const SVC_ICONS=["\u25C8","\u25C8","\u25C8","\u25C8"];
const FLAG_ICONS=["\u{1F1EB}\u{1F1EE}","\u{1F1F8}\u{1F1EA}","\u{1F1EC}\u{1F1E7}"];

const LEGAL={
terms:`<h2>Terms of Service</h2><p class="leg-up">Last updated: February 2026 Â· Aureum Private Office, Luxembourg</p>
<h3>1. About Aureum</h3><p>Aureum Private Office is an independent wealth concierge service. We provide competitive sourcing of bank and insurance wrapper proposals, bespoke portfolio reporting, independent performance benchmarking, and market insights via WhatsApp.</p><p><strong>Aureum is not a licensed investment firm.</strong> We do not provide investment advice, personal recommendations, or portfolio management. All reporting is informational.</p>
<h3>2. Service Scope</h3><p><strong>What we do:</strong> Collect your profile, present your anonymized profile to competing banks, facilitate introductions and meetings, receive portfolio reports under power of attorney, produce bespoke reports, and provide market estimates via WhatsApp.</p><p><strong>What we do not do:</strong> Provide investment advice, execute transactions, access accounts via API/PSD2, manage portfolios, guarantee outcomes, or act as an insurance intermediary.</p>
<h3>3. Eligibility</h3><p>Available to individuals and entities with investable assets of EUR 250,000+. Under EUR 1M: Finland. EUR 1M+: Luxembourg, UK. EUR 3M+: Switzerland, UAE. EUR 5M+: Monaco, Singapore.</p>
<h3>4. Fees</h3><p>Annual fee tiers: <strong>0.15%</strong> for portfolios up to \u20AC2M, <strong>0.10%</strong> for \u20AC2\u201315M, <strong>0.05%</strong> for \u20AC15M+. Minimum \u20AC500/year. Paid quarterly via standing order. No hidden fees, no commissions, no kickbacks.</p>
<h3>5. Power of Attorney</h3><p>A limited PoA authorizes your bank to share portfolio reports with Aureum and execute a quarterly standing order for our fee. The PoA does not authorize transactions, transfers, or any other account access. Either party may revoke with 30 days\u2019 notice.</p>
<h3>6. Language</h3><p>All services available in Finnish, Swedish, or English \u2014 including banker matching, reports, WhatsApp insights, and meeting facilitation.</p>
<h3>7. No Guarantee of Results</h3><p>Aureum does not guarantee any specific number of proposals, fee reductions, or investment returns. Past performance does not predict future results.</p>
<h3>8. Confidentiality</h3><p>All client information is strictly confidential. Your identity is not shared with banks during initial sourcing \u2014 only your anonymized profile.</p>
<h3>9. Termination</h3><p>Either party may terminate with 30 days\u2019 written notice. The PoA is revoked, standing order cancelled, and all reports provided to you. Current-quarter fees are non-refundable.</p>
<h3>10. Limitation of Liability</h3><p>Aureum provides informational services only. We are not liable for investment decisions, actions of third parties, market losses, or indirect damages.</p>
<h3>11. Governing Law</h3><p>These terms are governed by Luxembourg law.</p>
<h3>12. Regulatory Status</h3><p>Aureum is not licensed as an investment advisor, portfolio manager, or insurance intermediary. Our services are structured outside MiFID II, PSD2, and IDD regulation.</p>`,
privacy:`<h2>Privacy Policy</h2><p class="leg-up">Last updated: February 2026 Â· Data Controller: Aureum Private Office, Luxembourg Â· Contact: noah@aureumprivateoffice.com</p>
<h3>1. What We Collect</h3><p><strong>Identity:</strong> Name, nationality, date of birth. <strong>Contact:</strong> Email, phone, address. <strong>Financial:</strong> Investable assets, bank relationships, portfolio valuations. <strong>Professional:</strong> Occupation, source of wealth. <strong>Preferences:</strong> Jurisdictions, language, reporting frequency. <strong>Communications:</strong> Onboarding and WhatsApp messages.</p>
<h3>2. Why We Collect It</h3><p>Onboarding, sourcing proposals, producing reports, benchmarking, WhatsApp insights \u2014 all under GDPR Article 6(1)(b) (contract performance) or Article 6(1)(f) (legitimate interest).</p>
<h3>3. Portfolio Data</h3><p>Your bank provides periodic reports under a limited PoA. We do not access accounts via API, PSD2, or automated retrieval. All data is received as document-based reports.</p>
<h3>4. Who We Share With</h3><p><strong>Banks:</strong> Anonymized profile only during sourcing. Identity disclosed only with your authorization. <strong>Your bank:</strong> Shares reports with us under PoA. <strong>Service providers:</strong> GDPR-compliant, EU-based hosting and tools. <strong>We never sell, rent, or trade your data.</strong></p>
<h3>5. Security</h3><p>Encrypted storage on EU servers. Access restricted to authorized personnel. End-to-end encryption for sensitive communications. Data retained for service duration plus 7 years.</p>
<h3>6. Your Rights (GDPR)</h3><p>Access, rectify, erase, restrict, port, or object to your data processing. Withdraw consent at any time. Contact noah@aureumprivateoffice.com \u2014 we respond within 30 days.</p>
<h3>7. Supervisory Authority</h3><p>You may lodge a complaint with the CNPD (Commission nationale pour la protection des donn\u00E9es) or your local data protection authority.</p>
<h3>8. Changes</h3><p>Material changes communicated directly to active clients.</p>`
};

// FINNISH ARTICLES
const ARTICLES_FI=[
{title:"Miksi Suomi ensin?",
sub:"Suomalaisuudesta, suomalaisten palvelemisesta ja siitÃ¤, miksi tÃ¤mÃ¤ markkina merkitsee enemmÃ¤n kuin sen koko antaa ymmÃ¤rtÃ¤Ã¤.",
date:"Helmikuu 2026",
body:`<p>Minulta kysytÃ¤Ã¤n tÃ¤tÃ¤ usein â€“ yleensÃ¤ kansainvÃ¤listen sijoittajien tai yhteistyÃ¶kumppaneiden toimesta: "Miksi Suomi? Se on pieni markkina. Miksi et aloittanut Lontoosta, ZÃ¼richistÃ¤ tai Luxemburgista?"</p>
<p>Se on hyvÃ¤ kysymys.</p>
<p>Ja vastaus on samaan aikaan yksinkertainen ja henkilÃ¶kohtainen.</p>
<p>Koska olen suomalainen. Ja koska Suomi ansaitsee parempaa.</p>
<blockquote>"Koti ei ole koordinaatteja."</blockquote>
<p>Olen kasvanut monessa paikassa. Synnyin Yhdysvalloissa, vietin lapsuusvuosia JyvÃ¤skylÃ¤ssÃ¤ ja HelsingissÃ¤ ja olen asunut suuren osan aikuiselÃ¤mÃ¤stÃ¤ni Luxemburgissa.</p>
<p>SiitÃ¤ huolimatta Suomi on aina tuntunut kodilta.</p>
<p>Ei niinkÃ¤Ã¤n siksi, missÃ¤ synnyin tai missÃ¤ asun, vaan siksi missÃ¤ omat ihmiset ovat. SiellÃ¤ missÃ¤ kieli tuntuu luonnolliselta, eikÃ¤ siltÃ¤ ettÃ¤ sitÃ¤ joutuisi koko ajan kÃ¤Ã¤ntÃ¤mÃ¤Ã¤n pÃ¤Ã¤ssÃ¤Ã¤n. MissÃ¤ ei tarvitse selittÃ¤Ã¤ pieniÃ¤ asioita: miksi kengÃ¤t jÃ¤tetÃ¤Ã¤n eteiseen, miksi saunassa ollaan hiljaa, miksi perjantai-illan voi aivan hyvin viettÃ¤Ã¤ yksin kotona â€“ eikÃ¤ siinÃ¤ ole mitÃ¤Ã¤n outoa.</p>
<p>Molemmat vanhempani ovat suomalaisia. Sukulaiseni asuvat HelsingissÃ¤, JyvÃ¤skylÃ¤ssÃ¤, Yhdysvalloissa ja Luxemburgissa. KesÃ¤t mÃ¶killÃ¤ jÃ¤rven rannalla, jonka nimeÃ¤ en vielÃ¤kÃ¤Ã¤n osaa lausua oikein, mutta jossa olen uinut viisivuotiaasta asti. KeittiÃ¶npÃ¶ydÃ¤n keskustelut, joissa kieli vaihtuu suomesta englantiin kesken lauseen, koska se on meille luontevaa.</p>
<p>Ã„idinkieleni on suomi. Puhun useita kieliÃ¤, mutta suomi on kieli, jolla ajattelen. Se on kieli, jolla vaikeat asiat tuntuvat ymmÃ¤rrettÃ¤viltÃ¤. Se on kieli, joka tuntuu kodilta.</p>
<p>Kun pÃ¤Ã¤tin perustaa Aureumin, olisin voinut aloittaa lÃ¤hes mistÃ¤ tahansa. Luxemburgista, jossa asun. Lontoosta, jossa raha liikkuu. ZÃ¼richistÃ¤, jossa pankit ovat.</p>
<p>Mutta aloitin Suomesta. En siksi, ettÃ¤ se olisi suurin markkina, vaan siksi ettÃ¤ se on minun markkinani. Minun ihmiseni.</p>
<p>Ja koska vuosien aikana, seurattuani suomalaisten sijoittajien asemaa sivusta, mittani tuli tÃ¤yteen.</p>
<blockquote>"Hinnoitteluongelma, josta harva puhuu."</blockquote>
<p>TÃ¤ssÃ¤ on asia, jota monet suomalaiset eivÃ¤t tiedÃ¤: Suomessa maksetaan Euroopan korkeimpiin kuuluvia yksityispankkipalkkioita.</p>
<p>Ei siksi, ettÃ¤ pankit olisivat ahneita. Suomalaiset pankit ovat vakaita, hyvin johdettuja ja tarjoavat usein erinomaista palvelua. SyynÃ¤ on markkinan koko.</p>
<p>Pieni markkina tarkoittaa vÃ¤hemmÃ¤n kilpailua. Ja kun kilpailua on vÃ¤hemmÃ¤n, hinnat eivÃ¤t laske samalla tavalla kuin suurissa finanssikeskuksissa.</p>
<p>Kahden miljoonan euron salkku Suomessa maksaa helposti 1,2â€“1,5 prosenttia vuodessa, kun huomioidaan kaikki kulut: hallinnointi, rahastokulut, sÃ¤ilytys, valuuttamarginaalit ja transaktiot. Sama salkku Luxemburgissa on tyypillisesti 0,7â€“0,9 prosenttia. Lontoossa tai ZÃ¼richissÃ¤ usein samaa tasoa â€“ joskus alempaa, erityisesti yli viiden miljoonan euron varallisuudessa.</p>
<p>Ero ei ole palvelun laadussa. Ero on markkinadynamiikassa.</p>
<p>Luxemburgissa kilpailee yli sata yksityispankkia. ZÃ¼rich on yksi maailman syvimmistÃ¤ varainhoitokeskuksista. Kilpailu pakottaa lÃ¤pinÃ¤kyvyyteen ja hillitsee hinnoittelua. Suomessa todellisia vaihtoehtoja on vain muutama.</p>
<p>Ja kun olet yrittÃ¤jÃ¤ HelsingissÃ¤ tai JyvÃ¤skylÃ¤ssÃ¤, jolla on miljoona, kolme tai vaikka kymmenen miljoonaa euroa, neuvotteluvoimasi on rajallinen. Pankki tietÃ¤Ã¤, ettÃ¤ et todennÃ¤kÃ¶isesti halua monimutkaisia rakenteita useaan maahan. EttÃ¤ et ehkÃ¤ puhu saksaa tai ranskaa riittÃ¤vÃ¤n sujuvasti. EttÃ¤ haluat asioida suomeksi.</p>
<p>NiinpÃ¤ hinnoittelu pysyy korkeana. Ei kohtuuttomana â€“ mutta korkeana. Ja useimmat hyvÃ¤ksyvÃ¤t sen, koska eivÃ¤t tiedÃ¤ miltÃ¤ vaihtoehto nÃ¤yttÃ¤Ã¤.</p>
<p>MinÃ¤ tiedÃ¤n. Olen katsonut sitÃ¤ vuosia Luxemburgista kÃ¤sin.</p>
<blockquote>"PÃ¤Ã¤sy ei saa olla etuoikeus."</blockquote>
<p>Se mikÃ¤ minua hÃ¤iritsee eniten, on tÃ¤mÃ¤: Suomen kaikkein varakkaimmilla â€“ niillÃ¤, joilla on 20, 50 tai 100 miljoonaa euroa â€“ on jo pÃ¤Ã¤sy parempiin ehtoihin. HeillÃ¤ on neuvonantajia, family officeja ja useita pankkisuhteita eri maissa. He kilpailuttavat, neuvottelevat ja saavat institutionaalisen hinnoittelun.</p>
<p>Mutta jos olet menestyvÃ¤ yrittÃ¤jÃ¤ Tampereelta, joka myi yrityksensÃ¤ kolmella miljoonalla eurolla, olet pitkÃ¤lti omillasi. Tai lÃ¤Ã¤kÃ¤ri Oulusta, jolla on 800 000 euroa sÃ¤Ã¤stÃ¶jÃ¤ ja halu varmistaa hyvÃ¤ elÃ¤keaika. Saat vÃ¤hittÃ¤ishinnoittelun ja geneeriset ratkaisut.</p>
<p>Se ei ole oikein.</p>
<p>Tieto siitÃ¤, ettÃ¤ parempi hinnoittelu ja paremmat ehdot ovat olemassa, ei saisi olla vain harvojen etuoikeus. Kyky vertailla pankkeja ei saisi vaatia valmiita verkostoja tai kalliita konsultteja.</p>
<p>Suomi on tÃ¤ynnÃ¤ ihmisiÃ¤, jotka ovat rakentaneet varallisuutensa itse: yrittÃ¤jiÃ¤, asiantuntijoita, sijoittajia. He ansaitsevat saman lÃ¤pinÃ¤kyvyyden ja neuvotteluvoiman kuin joku GenevessÃ¤ saa automaattisesti.</p>
<p>SitÃ¤ varten Aureum on olemassa.</p>
<blockquote>"Pieni markkina, suuri vaikutus."</blockquote>
<p>Suomessa on noin 5,5 miljoonaa ihmistÃ¤. HeistÃ¤ ehkÃ¤ 50 000â€“100 000:lla on merkittÃ¤vÃ¤Ã¤ sijoitettavaa varallisuutta. Se on pieni markkina. Ja juuri siksi se on erinomainen paikka aloittaa.</p>
<p>PienessÃ¤ maassa tieto leviÃ¤Ã¤ nopeasti. Luottamus kulkee ihmisten kautta. Jos yksi asiakas HelsingissÃ¤ saa selkeÃ¤mmÃ¤n kokonaiskuvan, paremmat ehdot ja sÃ¤Ã¤stÃ¤Ã¤ merkittÃ¤vÃ¤sti palkkioissa, hÃ¤n kertoo siitÃ¤ eteenpÃ¤in. Se on Suomen vahvuus.</p>
<p>Rakentaisin mieluummin jotain merkityksellistÃ¤ Suomeen kuin jotain suurta ja kasvotonta muualle. Jos Aureum auttaa muutamaa sataa suomalaista perhettÃ¤ saamaan parempaa pankkitoimintaa seuraavien vuosien aikana, se merkitsee minulle enemmÃ¤n kuin miljardien hallinnointi ihmisille, joita en koskaan tapaa.</p>
<p>TÃ¤mÃ¤ ei ole hyvÃ¤ntekevÃ¤isyyttÃ¤. TÃ¤mÃ¤ on minulle henkilÃ¶kohtaista.</p>
<blockquote>"YmmÃ¤rrÃ¤mme suomalaisen kulttuurin."</blockquote>
<p>Suomalaiset sijoittajat ovat usein maltillisia. He arvostavat vakautta, suunnitelmallisuutta ja rehellisyyttÃ¤. He eivÃ¤t innostu suurista lupauksista tai markkinointipuheesta. Ja jos suomalainen asiakas on tyytymÃ¤tÃ¶n, hÃ¤n harvoin valittaa. HÃ¤n kestÃ¤Ã¤ hiljaa.</p>
<p>Juuri siksi Aureum toimii. Me kysymme vaikeat kysymykset. PyydÃ¤mme erittelyt. Vertailemme ja neuvottelemme. Sinun ei tarvitse olla vaativa tai Ã¤Ã¤nekÃ¤s. RiittÃ¤Ã¤, ettÃ¤ sanot kyllÃ¤ paremmille ehdoille, kun tuomme ne sinulle.</p>
<blockquote>"KielellÃ¤ on merkitystÃ¤."</blockquote>
<p>Kun puhutaan perinnÃ¶stÃ¤, elÃ¤kkeestÃ¤ tai sukupolvien yli ulottuvasta varallisuudesta, haluat puhua omalla kielellÃ¤si. Suomeksi.</p>
<p>Aureum lÃ¶ytÃ¤Ã¤ suomenkielisiÃ¤ pankkiireja myÃ¶s kansainvÃ¤lisistÃ¤ pankeista. IhmisiÃ¤, jotka ymmÃ¤rtÃ¤vÃ¤t paitsi kielen, myÃ¶s sen mitÃ¤ suomalainen tarkoittaa sanoessaan "ehkÃ¤".</p>
<p>Kieli ei ole vain sanoja. Se on luottamusta.</p>
<blockquote>"Suomi ensin."</blockquote>
<p>Aloitimme Suomesta. Emme siksi, ettÃ¤ se olisi helpointa, vaan siksi ettÃ¤ se on oikein.</p>
<p>TÃ¤Ã¤ltÃ¤ kÃ¤sin laajennamme aikanaan muualle â€“ Pohjoismaihin, Baltiaan, sinne missÃ¤ samat ongelmat toistuvat. Mutta ensin koti.</p>
<p>Koska tÃ¤mÃ¤ ei ole vain liiketoimintaa. TÃ¤mÃ¤ on korjaus.</p>
<p>Liian kauan suomalaiset sijoittajat ovat hyvÃ¤ksyneet korkeat palkkiot ja rajalliset vaihtoehdot ikÃ¤Ã¤n kuin ne olisivat luonnonlaki. Liian kauan pÃ¤Ã¤sy globaaliin yksityispankkitoimintaan on ollut varattu niille, joilla oli jo valmiit yhteydet ZÃ¼richiin tai Geneveen.</p>
<p>Se aika on ohi.</p>
<p>Aureum on olemassa tasaamaan pelikenttÃ¤Ã¤. Tuomaan institutionaalisen tason pankkitoiminnan lÃ¤pinÃ¤kyvyyden kenelle tahansa, jolla on merkittÃ¤vÃ¤Ã¤ varallisuutta â€“ ei vain harvoille.</p>
<p>Ei siksi, ettÃ¤ se olisi helppoa. Vaan siksi, ettÃ¤ se on oikein.</p>
<p><em>Koti on siellÃ¤, missÃ¤ sydÃ¤n on. Ja minun sydÃ¤meni on Suomessa.</em></p>`},

{title:"Miksi Aureum on teknologiayritys",
sub:"Varallisuuden ymmÃ¤rtÃ¤minen molemmista kulmista",
date:"Helmikuu 2026",
body:`<p>Muistan tarkalleen hetken, jolloin ymmÃ¤rsin mikÃ¤ oli vialla. Istuin perhepÃ¤ivÃ¤llisellÃ¤ Luxemburgissa. IsÃ¤ni oli juuri voittanut merkittÃ¤vÃ¤n uuden asiakkaan yksinkertaisella tavalla: hÃ¤n nÃ¤ytti kokonaiskustannukset selkeÃ¤sti.</p>
<p>Kilpaileva pankki tarjosi "0,65 % hallinnointipalkkion". IsÃ¤ni analyysi osoitti, ettÃ¤ asiakas maksoi todellisuudessa 1,45 % kokonaiskuluina. HÃ¤nen tarjouksensa? 0,85 % - korkeampi hallinnointipalkkio, mutta lÃ¤pinÃ¤kyvÃ¤. Kaikki sisÃ¤ltÃ¤en. Asiakas vaihtoi pankkia kahdessa viikossa.</p>
<blockquote>"Sen ei pitÃ¤isi olla kilpailuetu. Sen pitÃ¤isi olla normaali."</blockquote>
<p>Kasvoin oudossa risteyskohdassa. Toisella puolella: sveitsilÃ¤inen yksityispankkitoiminta - suhdelÃ¤htÃ¶inen, sukupolvia kestÃ¤vÃ¤Ã¤n luottamukseen rakentuva. Toisella puolella: institutionaalinen pÃ¤Ã¤omasijoittaminen - hallintokehyksiÃ¤, mandaattikuria, systemaattista valvontaa.</p>
<p>NÃ¤in saman varallisuuden kohdeltavan tÃ¤ysin eri tavalla. Institutionaalisilla oli kojelautoja, dataa ja vastuullisuutta. YksityisillÃ¤ oli neljÃ¤nnesvuosittaiset PDF:t ja luottamus. Kuilu ei johtunut Ã¤lykkyydestÃ¤ vaan infrastruktuurista.</p>
<blockquote>"Ongelma ei ole ihmisissÃ¤. Se on teknologiassa."</blockquote>
<p>Yksityispankkitoiminnassa on maailmanluokan ammattilaisia ja erinomaisia tuotteita. Mutta jÃ¤rjestelmÃ¤t â€“ teknologia, jonka pitÃ¤isi tehdÃ¤ tÃ¤stÃ¤ lÃ¤pinÃ¤kyvÃ¤Ã¤ â€“ ovat hÃ¤mmÃ¤styttÃ¤vÃ¤n vanhentuneita.</p>
<p>Aureum Private Office ei kilpaile pankkien kanssa. Rakensimme teknologiavetoisen alustan, joka toimii pankkien ylÃ¤puolella. Ajattele meitÃ¤ varallisuutesi kÃ¤yttÃ¶jÃ¤rjestelmÃ¤nÃ¤. Pankit ovat sovelluksia - me olemme alusta joka kokoaa, analysoi ja tarjoaa selkeyden.</p>
<p>Emme ole jumissa 1990-luvun jÃ¤rjestelmissÃ¤. KÃ¤ytÃ¤mme parhaita saatavilla olevia analytiikkatyÃ¶kaluja, institutionaalisia riskimalleja ja turvallista modernia viestintÃ¤Ã¤. Teknologia mahdollistaa reaaliaikaiset nÃ¤kemykset - ei neljÃ¤nnesvuosittaisia PDF-tiedostoja.</p>
<p>Aureumin erityisyys: ymmÃ¤rrÃ¤mme molempia maailmoja. TiedÃ¤mme miten yksityispankit hinnoittelevat, missÃ¤ kulut piiloutuvat ja miten neuvottelut toimivat. Samalla ymmÃ¤rrÃ¤mme miten modernit alustat skaalaantuvat ja miten datasta uutetaan nÃ¤kemystÃ¤.</p>
<blockquote>"Yksityisvarallisuus ei tarvitse lisÃ¤Ã¤ rahastoja. Se tarvitsee parempaa infrastruktuuria."</blockquote>
<p>Koska olemme teknologiayritys - emme pankki - kannustimet ovat yksinkertaiset: emme ansaitse palkkioita tuotteista, emme hyÃ¶dy monimutkaisuudesta. Palkkiomme on lÃ¤pinÃ¤kyvÃ¤ ja yhdensuuntainen asiakkaan edun kanssa.</p>
<p>Vuonna 2026 varallisuutesi ansaitsee parempaa kuin hajallaan olevia PDF-tiedostoja. Se ansaitsee mitÃ¤ institutionaalisilla sijoittajilla on ollut vuosikymmeniÃ¤: selkeyden, datan ja vastuullisuuden.</p>`},

{title:"Rakenteellisen vertailun kurinalaisuus",
sub:"Institutionaalista kurinalaisuutta yksityisvarallisuuteen",
date:"Helmikuu 2026",
body:`<p>Yksityisvarallisuudessa suorituskyky herÃ¤ttÃ¤Ã¤ huomion. Rakenne harvoin. Markkinat liikkuvat, strategiat vaihtuvat, otsikot muuttuvat. Silti pitkÃ¤llÃ¤ aikavÃ¤lillÃ¤ tuloksia muovaavat ennustettavimmin ei volatiliteetti vaan arkkitehtuuri: sÃ¤ilytysjÃ¤rjestelyt, kulukerrokset, toteutuksen laatu.</p>
<blockquote>"Tuotot ovat todennÃ¤kÃ¶isyyksiÃ¤. Kulut ovat matematiikkaa."</blockquote>
<p>Institutionaaliset sijoittajat vertailevat systemaattisesti. He neuvottelevat sÃ¤ilytyssopimukset uudelleen, kvantifioivat kokonaiskulukerrokset ja arvioivat rakenteita uudelleen olosuhteiden muuttuessa. Tarkastelu on rakennettu jÃ¤rjestelmÃ¤Ã¤n.</p>
<p>Yksityissijoittajat sitÃ¤ vastoin yllÃ¤pitÃ¤vÃ¤t usein pitkÃ¤aikaisia pankkisuhteita, jotka jÃ¤Ã¤vÃ¤t rakenteellisesti tutkimatta vuosiksi. Ei osaamisen puutteen vuoksi, vaan koska vertailua ei ole institutionalisoitu yksityisvarallisuudessa.</p>
<p>Aureum perustettiin juuri tuon kuilun kuromiseksi. Yritys ei anna sijoitusneuvontaa, ei jaa tuotteita, ei edusta pankkeja. Sen sijaan se keskittyy yksinomaan riippumattomaan rakenneanalyysiin ja vertailevaan benchmarkingiin.</p>
<blockquote>"Roolimme on analyyttinen. Emme ole tÃ¤Ã¤llÃ¤ korvaamassa pankkeja. Olemme tÃ¤Ã¤llÃ¤ tuomaan kurinalaista vertailua."</blockquote>
<p>Teknologinen infrastruktuuri on muuttanut yhtÃ¤lÃ¶n. YhtenÃ¤istetyt raportointijÃ¤rjestelmÃ¤t, alustojen vÃ¤linen benchmarking ja strukturoitu kustannusanalyysi mahdollistavat nyt riippumattoman vertailun tehokkaasti ilman institutionaalista hallinnollista rasitetta.</p>
<p>Periaate skaalaantuu. SekÃ¤ 400 000 euron salkku ettÃ¤ 40 miljoonan rakenne hyÃ¶tyvÃ¤t kurinalaisesta vertailusta. Mittakaava vaihtelee; logiikka ei.</p>
<blockquote>"Valvonta ei ole varallisuustason funktio. Se on vakavuuden funktio."</blockquote>
<p>Luottamuksen ja todentamisen tulisi kulkea rinnakkain. Vertailun ei pitÃ¤isi olla poikkeuksellista - sen pitÃ¤isi olla rutiinia. Parempia tuottoja ei voida taata. Tarpeettomat alhaisemmat kulut voidaan tunnistaa. Rakenteellinen yhdensuuntaisuus voidaan todentaa.</p>
<blockquote>"Yksityisvarallisuus ei tarvitse disruptiota. Se tarvitsee rakennetta."</blockquote>
<p>Ja rakennetta, toisin kuin markkinoita, voidaan tutkia.</p>`},

{title:"IkÃ¤, luottamus ja valvonnan arkkitehtuuri",
sub:"Miksi nuori perustaja johtaa teknologiavetoista valvontaa",
date:"Helmikuu 2026",
body:`<p>"Olet suhteellisen nuori. Miksi vakavien sijoittajien pitÃ¤isi luottaa sinuun?" Se on reilu kysymys. Luottamus varainhallinnas sa on historiallisesti yhdistetty ikÃ¤Ã¤n - harmaantuviin hiuksiin, pitkÃ¤Ã¤n palveluvuosiin, vakiintuneisiin suhteisiin.</p>
<blockquote>"En pyydÃ¤ sijoittajia luottamaan markkina-ennusteisiini. PyydÃ¤n heitÃ¤ tutkimaan mitattavia rakenteita."</blockquote>
<p>Aureum ei anna sijoitusneuvontaa. Se ei valitse arvopapereita. Sen rooli on analyyttinen: kulukerrosten yhdistÃ¤minen, sÃ¤ilytysjÃ¤rjestelyjen benchmarking, alustojen vertailu ja rakenteellisen tehokkuuden kvantifiointi.</p>
<p>Altistuminen yksityispankkitoimintaan alkoi varhain. IsÃ¤ni vietti lÃ¤hes kaksi vuosikymmentÃ¤ Sveitsin yksityispankissa neuvoen Suomen varakkaimpiin kuuluvia perheitÃ¤. Ã„itini rakensi uransa institutionaalisessa pÃ¤Ã¤omasijoittamisessa, jossa hallintokehykset ovat perustavanlaatuisia. Kontrasti muokkasi ymmÃ¤rrystÃ¤ siitÃ¤, missÃ¤ yksityisvarallisuus jÃ¤Ã¤ jÃ¤lkeen.</p>
<p>MÃ¤Ã¤rittÃ¤vÃ¤ etu on teknologinen osaaminen. Moderni benchmarking, automatisoitu kustannusten kokoaminen ja strukturoitu raportointi vaativat jÃ¤rjestelmÃ¤suunnittelua. Tuo sukupolvinen osaaminen ei ole kosmeettista - se on toiminnallista.</p>
<blockquote>"Rakennamme infrastruktuuria. TÃ¤mÃ¤ ei ole perinteinen neuvontatoimisto. Se on teknologian mahdollistama valvontakerros."</blockquote>
<p>Institutionaalisilla on jo konsultit ja datajÃ¤rjestelmÃ¤t. Yksityissijoittajilla ei ollut - kunnes teknologia teki sen mahdolliseksi. Aureum on tuossa risteyksessÃ¤: institutionaalinen logiikka, toimitettu modernin infrastruktuurin kautta.</p>
<p>Luottamus ei saisi olla ankkuroitu yksin ikÃ¤Ã¤n vaan yhdensuuntaisuuteen ja lÃ¤pinÃ¤kyvyyteen. Kysymys on tuottaako jÃ¤rjestelmÃ¤ mitattavaa selkeyttÃ¤. Kokemus merkitsee, mutta niin merkitsee myÃ¶s modernisointi.</p>`},

{title:"Kielikuilu kansainvÃ¤lisessÃ¤ pankkitoiminnassa",
sub:"Ã„idinkielellÃ¤ keskustelemisen merkitys",
date:"Helmikuu 2026",
body:`<p>On tietynlainen tapaaminen, joka tapahtuu tuhansia kertoja joka vuosi. Suomalainen yrittÃ¤jÃ¤ istuu vastapÃ¤Ã¤tÃ¤ asiakasvastaavaa GenevessÃ¤ tai Luxemburgissa. Pankkiiri puhuu sujuvasti englantia. Keskustelu on ammattimaista. Ja silti jotain olennaista katoaa.</p>
<blockquote>"Lastesi perinnÃ¶stÃ¤ keskusteleminen kolmannella kielellÃ¤si ei ole sama asia kuin sen keskusteleminen omalla Ã¤idinkielellÃ¤si."</blockquote>
<p>Varallisuus ei ole abstrakti aihe. Se kantaa perheen historian painoa, sukupolvien suunnittelua, huolia jotka eivÃ¤t kÃ¤Ã¤nny helposti kulttuuristen rajojen yli. PÃ¤Ã¤tÃ¶s siirtÃ¤Ã¤ pÃ¤Ã¤omaa rajojen yli ei ole puhtaasti taloudellinen - se on henkilÃ¶kohtainen.</p>
<p>Kotimaiset pankit jakavat usein omia rahastojaan - sisÃ¤isiÃ¤ rahastoja, joiden kulusuhteet ovat korkeammat kuin vastaavien institutionaalisten osuusluokkien. KansainvÃ¤liset yksityispankit toimivat eri tavalla. Monet tarjoavat kaikki mukaan lukevaa hinnoittelua ja pÃ¤Ã¤syn institutionaalisiin osuusluokkiin.</p>
<p>Mutta on toinenkin ulottuvuus: kieli. Suomenkielinen pankkiiri GenevessÃ¤ tai Luxemburgissa ei ole vain mukavuustekijÃ¤ - se on rakenteellinen etu.</p>
<p>Kun keskustelet elÃ¤kesuunnitelmasta tai varallisuusveron minimoimisesta, haluat tehdÃ¤ sen suomeksi. Haluat tietÃ¤Ã¤, ettÃ¤ kun sanot "perintÃ¶vero", vastapÃ¤Ã¤ssÃ¤ oleva henkilÃ¶ ymmÃ¤rtÃ¤Ã¤ vÃ¤littÃ¶mÃ¤sti sekÃ¤ sanan ettÃ¤ sen painon.</p>
<p>Useimmat kansainvÃ¤liset yksityispankit lÃ¶ytÃ¤vÃ¤t jonkun, joka puhuu "jonkin verran suomea". Se ei ole riittÃ¤vÃ¤Ã¤. Aureum lÃ¶ytÃ¤Ã¤ suomenkielisiÃ¤ pankkiireja kansainvÃ¤lisistÃ¤ pankeista - ihmisiÃ¤, jotka ymmÃ¤rtÃ¤vÃ¤t ettÃ¤ kun suomalainen asiakas sanoo "ehkÃ¤", se saattaa tarkoittaa ei.</p>
<blockquote>"Kieli ei ole vain sanoja. Se on luottamusta."</blockquote>
<p>Kun asiakas ja pankkiiri puhuvat samaa kieltÃ¤ - todella samaa kieltÃ¤ - viestintÃ¤ on tarkempaa, vÃ¤Ã¤rinkÃ¤sitykset vÃ¤henevÃ¤t ja luottamus syvenee. Varallisuudenhallinnassa selkeys on arvokasta.</p>`},

{title:"Piilotetut kulut, joita pohjoismaiset sijoittajat eivÃ¤t koskaan nÃ¤e",
sub:"MitÃ¤ todella maksat",
date:"Helmikuu 2026",
body:`<p>"Pankkini veloittaa 0,65 % hallinnointipalkkiota. Se on kilpailukykyinen." Teknisesti totta - jos mittaat vain yhtÃ¤ kerrosta. Todellisuudessa useimmat maksavat 1,2-1,8 % kokonaiskuluista vuodessa. He eivÃ¤t vain tiedÃ¤ sitÃ¤, koska suurin osa kuluista on piilotettu.</p>
<blockquote>"Useimmat sijoittajat eivÃ¤t voi kvantifioida kokonaisomistuskustannustaan. Se ei ole vahinko."</blockquote>
<p>Kulukerrosten anatomia: 1) Hallinnointipalkkio (ainoa nÃ¤kyvÃ¤, 0,50-0,80%), 2) Valuuttakulut (suurin piilotettu, 0,30-1,00% jokaisessa konversiossa), 3) Taustalla olevat rahastokulut (0,20-0,60%), 4) SÃ¤ilytysmaksu (0,05-0,15%), 5) Transaktiokulut (0,10-0,20%), 6) Alusta- ja tilimaksut (0,05-0,10%).</p>
<p>Summaa nÃ¤mÃ¤ kerrokset, ja asiakas joka maksaa "0,65 %" hallinnointipalkkiota maksaa usein 1,20-1,80 % kokonaisefektiivisissÃ¤ kuluissa. 2Mâ‚¬ salkulla kymmenen vuoden aikana tuo piilotettu 0,60-1,15 % maksaa noin 120 000-230 000 euroa menetetyssÃ¤ kasvussa.</p>
<p>Pankit ansaitsevat miljardeja valuuttamarginaaleista juuri siksi, ettÃ¤ asiakkaat eivÃ¤t nÃ¤e niitÃ¤. Kotimaiset pankit kÃ¤yttÃ¤vÃ¤t usein omia sisÃ¤isiÃ¤ rahastojaan korkeammilla kuluilla. KansainvÃ¤liset tarjoavat kaikki mukaan lukevaa hinnoittelua ja pÃ¤Ã¤syn institutionaalisiin osuusluokkiin.</p>
<blockquote>"Kysymys ei ole onko pankkisi hyvÃ¤. Kysymys on onko rakenteesi tehokas."</blockquote>
<p>Aureumin lÃ¤hestymistapa: kvantifioimme jokaisen kerroksen - ilmoitetun, arvioidun ja piilotetun. EsitÃ¤mme kokonaismÃ¤Ã¤rÃ¤n kilpailevien tarjousten rinnalla.</p>
<p>Yhteisvoima-ohjelma: yksittÃ¤iset mandaatit esitetÃ¤Ã¤n pankeille osana suurempaa pohjoismaisten sijoittajien kokonaisvarallisuutta. Jokainen asiakas yllÃ¤pitÃ¤Ã¤ tÃ¤ysin erillisiÃ¤ tilejÃ¤, mutta pankin nÃ¤kÃ¶kulmasta suhde edustaa merkittÃ¤vÃ¤Ã¤ volyymiÃ¤. 1Mâ‚¬ mandaatti osana 25Mâ‚¬ kokonaisuutta saa institutionaalista huomiota - paremmat palkkioaikataulut, pÃ¤Ã¤sy parempiin osuusluokkiin.</p>
<blockquote>"Yhteisvoima tarkoittaa, ettÃ¤ jokainen asiakas hyÃ¶tyy verkoston mittakaavasta sÃ¤ilyttÃ¤en tÃ¤ydellisen yksilÃ¶llisen luottamuksellisuuden."</blockquote>
<p>Asiakkaat, jotka olettivat maksavansa 0,65 %, huomaavat maksavansa 1,30 %. Aureumin kautta: tarjouksia 0,60-0,80 % kaikki mukaan lukien. Laskenta ei ole monimutkaista, mutta sitÃ¤ harvoin tehdÃ¤Ã¤n. Aureum on olemassa tekemÃ¤Ã¤n se.</p>`}
];

// SWEDISH ARTICLES (condensed professional versions)
const ARTICLES_SV=[
{title:"VarfÃ¶r Finland fÃ¶rst?",
sub:"Om att vara finlÃ¤ndare och att tjÃ¤na finlÃ¤ndare",
date:"Februari 2026",
body:`<p>Jag fÃ¥r ofta frÃ¥gan: "VarfÃ¶r Finland? Det Ã¤r en liten marknad. VarfÃ¶r bÃ¶rjade du inte i London, ZÃ¼rich eller Luxemburg?" Bra frÃ¥ga. Och svaret Ã¤r bÃ¥de enkelt och personligt.</p>
<p>Eftersom jag Ã¤r finlÃ¤ndare. Och eftersom Finland fÃ¶rtjÃ¤nar bÃ¤ttre.</p>
<blockquote>"Hemma Ã¤r inte koordinater."</blockquote>
<p>Jag vÃ¤xte upp mellan vÃ¤rldar - fÃ¶dd i USA, barndom i JyvÃ¤skylÃ¤ och Helsingfors, men stÃ¶rsta delen av livet i Luxemburg. Ã„ndÃ¥ har Finland alltid kÃ¤nts som hemma. Inte pÃ¥ grund av var jag fÃ¶ddes, utan pÃ¥ grund av var mina mÃ¤nniskor finns.</p>
<p>BÃ¥da mina fÃ¶rÃ¤ldrar Ã¤r finlÃ¤ndare. Mina slÃ¤ktingar bor i Helsingfors, JyvÃ¤skylÃ¤, USA och Luxemburg. Somrar vid stugan dÃ¤r jag har simmat sedan jag var fem. KÃ¶ksbordsamtal dÃ¤r sprÃ¥ket vÃ¤xlar frÃ¥n finska till engelska mitt i meningen.</p>
<p>Mitt modersmÃ¥l Ã¤r finska. Jag talar flera sprÃ¥k, men finska Ã¤r sprÃ¥ket jag tÃ¤nker pÃ¥. Det Ã¤r sprÃ¥ket som kÃ¤nns som hemma.</p>
<p>NÃ¤r jag grundade Aureum kunde jag ha bÃ¶rjat nÃ¤stan var som helst. Men jag bÃ¶rjade i Finland. Inte fÃ¶r att det Ã¤r stÃ¶rsta marknaden, utan fÃ¶r att det Ã¤r min marknad. Mina mÃ¤nniskor.</p>
<blockquote>"PrissÃ¤ttningsproblemet som fÃ¥ pratar om."</blockquote>
<p>I Finland betalas nÃ¥gra av Europas hÃ¶gsta privatbankavgifter. Inte fÃ¶r att bankerna Ã¤r giriga, utan pÃ¥ grund av marknadens storlek. En 2Mâ‚¬ portfÃ¶lj i Finland kostar lÃ¤tt 1,2-1,5% Ã¥rligen mot 0,7-0,9% i Luxemburg. Skillnaden Ã¤r marknadsdynamik - Luxemburg har Ã¶ver hundra konkurrerande banker.</p>
<p>Finlands rikaste har redan tillgÃ¥ng till bÃ¤ttre prissÃ¤ttning. Men om du Ã¤r en framgÃ¥ngsrik entreprenÃ¶r med 3Mâ‚¬, Ã¤r du pÃ¥ egen hand. Det Ã¤r inte rÃ¤tt. Finland Ã¤r fullt av mÃ¤nniskor som fÃ¶rtjÃ¤nar samma transparens som nÃ¥gon i GenÃ¨ve fÃ¥r automatiskt.</p>
<blockquote>"Liten marknad, stor inverkan."</blockquote>
<p>I ett litet land sprids information snabbt. Om en kund fÃ¥r bÃ¤ttre villkor, berÃ¤ttar hen vidare. Det Ã¤r styrkan. Jag skulle hellre bygga nÃ¥got meningsfullt i Finland Ã¤n nÃ¥got stort nÃ¥gon annanstans.</p>
<p>Vi bÃ¶rjade i Finland. Inte fÃ¶r att det Ã¤r lÃ¤ttast, utan fÃ¶r att det Ã¤r rÃ¤tt. HÃ¤rifrÃ¥n expanderar vi till Norden, Baltikum. Men fÃ¶rst hemma. FÃ¶r detta Ã¤r inte bara affÃ¤rer - det Ã¤r en korrigering. Den tiden dÃ¥ endast de rikaste hade global tillgÃ¥ng Ã¤r Ã¶ver.</p>
<p><em>Hemma Ã¤r dÃ¤r hjÃ¤rtat Ã¤r. Och mitt hjÃ¤rta Ã¤r i Finland.</em></p>`},

{title:"VarfÃ¶r Aureum Ã¤r ett teknikfÃ¶retag",
sub:"Teknik i kÃ¤rnan",
date:"Februari 2026",
body:`<p>Jag minns exakt Ã¶gonblicket. Min far vann en kund genom att visa totala kostnader transparent. Konkurrenten: "0,65% fÃ¶rvaltning". Analysen: 1,45% verkliga kostnader. Min fars erbjudande: 0,85% - transparent. Kunden bytte pÃ¥ tvÃ¥ veckor.</p>
<blockquote>"Det borde inte vara en konkurrensfÃ¶rdel. Det borde vara normalt."</blockquote>
<p>Jag vÃ¤xte upp i korsningen mellan schweizisk privatbankverksamhet och institutionell private equity. Samma fÃ¶rmÃ¶genhet - helt olika behandling. Klyftan berodde inte pÃ¥ intelligens utan infrastruktur. Institutionella hade dashboards och data. Privata hade kvartals-PDF:er och fÃ¶rtroende.</p>
<p>Problemet Ã¤r inte mÃ¤nniskorna. Det Ã¤r tekniken. Aureum konkurrerar inte med banker - vi byggde en plattform som fungerar ovanpÃ¥ dem. TÃ¤nk pÃ¥ oss som operativsystemet fÃ¶r din fÃ¶rmÃ¶genhet.</p>
<p>Vi Ã¤r inte fast i 90-talets system. Vi anvÃ¤nder bÃ¤sta verktygen och mÃ¶jliggÃ¶r realtidsinsikter - inte kvartalsrapporter. Vi fÃ¶rstÃ¥r bÃ¥da vÃ¤rldarna: privatbankverksamhet och modern teknik.</p>
<blockquote>"Privat fÃ¶rmÃ¶genhet behÃ¶ver inte fler fonder. Den behÃ¶ver bÃ¤ttre infrastruktur."</blockquote>
<p>FÃ¶r Ã¥r 2026 fÃ¶rtjÃ¤nar din fÃ¶rmÃ¶genhet vad institutionella har haft i decennier: klarhet, data och ansvarsskyldighet.</p>`},

{title:"Disciplinen i strukturell jÃ¤mfÃ¶relse",
sub:"Institutionell disciplin till privat fÃ¶rmÃ¶genhet",
date:"Februari 2026",
body:`<p>I privat fÃ¶rmÃ¶genhet vÃ¤cker prestation uppmÃ¤rksamhet. Struktur sÃ¤llan. Ã„ndÃ¥ formas resultat pÃ¥ lÃ¥ng sikt mest fÃ¶rutsÃ¤gbart av arkitektur, inte volatilitet.</p>
<blockquote>"Avkastning Ã¤r sannolikheter. Kostnader Ã¤r matematik."</blockquote>
<p>Institutionella investerare benchmarkar systematiskt. Privata upprÃ¤tthÃ¥ller relationer som fÃ¶rblir ogranskade i Ã¥ratal. Inte pÃ¥ grund av brist pÃ¥ expertis - jÃ¤mfÃ¶relse har inte institutionaliserats.</p>
<p>Aureum grundades fÃ¶r att Ã¶verbrygga klyftan. FÃ¶retaget fokuserar pÃ¥ oberoende strukturanalys och benchmarking. Teknisk infrastruktur mÃ¶jliggÃ¶r nu detta effektivt.</p>
<blockquote>"Ã–vervakning Ã¤r inte en funktion av fÃ¶rmÃ¶genhetsnivÃ¥. Det Ã¤r en funktion av seriositet."</blockquote>
<p>BÃ¤ttre avkastning kan inte garanteras. OnÃ¶digt hÃ¶gre kostnader kan identifieras. Strukturell samstÃ¤mmighet kan verifieras.</p>
<blockquote>"Privat fÃ¶rmÃ¶genhet behÃ¶ver inte disruption. Den behÃ¶ver struktur."</blockquote>
<p>Och struktur, till skillnad frÃ¥n marknader, kan granskas.</p>`},

{title:"Ã…lder, fÃ¶rtroende och Ã¶vervakningens arkitektur",
sub:"VarfÃ¶r en ung grundare leder teknikaktiverad Ã¶vervakning",
date:"Februari 2026",
body:`<p>"Du Ã¤r relativt ung. VarfÃ¶r skulle investerare lita pÃ¥ dig?" RÃ¤ttvis frÃ¥ga. Men Aureum byggs pÃ¥ strukturanalys, inte relationer.</p>
<blockquote>"Jag ber inte om fÃ¶rtroende fÃ¶r prognoser. Jag ber om granskning av mÃ¤tbara strukturer."</blockquote>
<p>Aureum ger inte investeringsrÃ¥dgivning. Dess roll Ã¤r analytisk: aggregera kostnadslager, benchmarka arrangemang, kvantifiera effektivitet.</p>
<p>Min exponering bÃ¶rjade tidigt. Min fars nÃ¤stan tvÃ¥ decennier vid schweizisk privatbank, min mors karriÃ¤r inom institutionell private equity. Kontrasten lÃ¤rde var privat fÃ¶rmÃ¶genhet halkar efter.</p>
<p>Den avgÃ¶rande fÃ¶rdelen Ã¤r teknisk kompetens. Modern benchmarking och automatiserad analys krÃ¤ver systemdesign. Institutionella har redan detta. Tekniken gÃ¶r det nu tillgÃ¤ngligt fÃ¶r privata.</p>
<blockquote>"Vi bygger infrastruktur. Detta Ã¤r inte traditionell rÃ¥dgivning. Det Ã¤r ett teknikaktiverat Ã¶vervakningslager."</blockquote>
<p>FÃ¶rtroende borde vara fÃ¶rankrat i samstÃ¤mmighet och transparens, inte endast Ã¥lder.</p>`},

{title:"SprÃ¥kgapet i internationell bankverksamhet",
sub:"ModersmÃ¥l spelar roll",
date:"Februari 2026",
body:`<p>Det finns en typ av mÃ¶te som sker tusentals gÃ¥nger Ã¥rligen. En finsk entreprenÃ¶r sitter mitt emot en rÃ¥dgivare i GenÃ¨ve. Bankiren talar flytande engelska. Samtalet Ã¤r professionellt. Ã„ndÃ¥ gÃ¥r nÃ¥got vÃ¤sentligt fÃ¶rlorat.</p>
<blockquote>"Att diskutera arv pÃ¥ ditt tredje sprÃ¥k Ã¤r inte samma sak."</blockquote>
<p>FÃ¶rmÃ¶genhet bÃ¤r familjens historia, generationers planering. Beslutet att flytta kapital Ã¶ver grÃ¤nser Ã¤r personligt, inte endast ekonomiskt.</p>
<p>Inhemska banker distribuerar ofta egna fonder med hÃ¶gre kostnader. Internationella banker erbjuder all-inclusive-prissÃ¤ttning och institutionell Ã¥tkomst. Men det finns en annan dimension: sprÃ¥k.</p>
<p>En finsktalande bankir Ã¤r inte bara bekvÃ¤mlighet - det Ã¤r en strukturell fÃ¶rdel. NÃ¤r du diskuterar pension eller arv vill du gÃ¶ra det pÃ¥ finska. Du vill veta att "perintÃ¶vero" fÃ¶rstÃ¥s omedelbart.</p>
<p>De flesta internationella banker hittar nÃ¥gon som talar "lite finska". Det rÃ¤cker inte. Aureum hittar finsktalande bankirer som fÃ¶rstÃ¥r att "kanske" kan betyda nej.</p>
<blockquote>"SprÃ¥k Ã¤r inte bara ord. Det Ã¤r fÃ¶rtroende."</blockquote>
<p>NÃ¤r kund och bankir talar samma sprÃ¥k - verkligen samma sprÃ¥k - Ã¤r kommunikationen exaktare och fÃ¶rtroendet djupare.</p>`},

{title:"De dolda kostnaderna nordiska investerare aldrig ser",
sub:"Vad du verkligen betalar",
date:"Februari 2026",
body:`<p>"Min bank tar 0,65% fÃ¶rvaltningsavgift." Tekniskt sant - om du mÃ¤ter ett lager. Verkligheten: de flesta betalar 1,2-1,8% totalt utan att veta det.</p>
<blockquote>"Flesta kostnader Ã¤r dolda."</blockquote>
<p>Kostnadslager: 1) FÃ¶rvaltningsavgift (synlig, 0,50-0,80%), 2) Valutamarginaler (stÃ¶rsta dolda, 0,30-1,00%), 3) Fondkostnader (0,20-0,60%), 4) FÃ¶rvaring (0,05-0,15%), 5) Transaktioner (0,10-0,20%), 6) Plattform (0,05-0,10%).</p>
<p>PÃ¥ 2Mâ‚¬ Ã¶ver tio Ã¥r kostar dolda 0,60-1,15% cirka 120 000-230 000â‚¬ i fÃ¶rlorad tillvÃ¤xt. Banker tjÃ¤nar miljarder pÃ¥ valutamarginaler eftersom kunder inte ser dem.</p>
<blockquote>"FrÃ¥gan Ã¤r inte om din bank Ã¤r bra. FrÃ¥gan Ã¤r om din struktur Ã¤r effektiv."</blockquote>
<p>Aureum kvantifierar varje lager. Collective Strength-programmet: individuella mandat presenteras som del av stÃ¶rre nordisk AUM. 1Mâ‚¬ som del av 25Mâ‚¬ fÃ¥r institutionell uppmÃ¤rksamhet - bÃ¤ttre villkor, Ã¥tkomst till bÃ¤ttre andelsklasser.</p>
<blockquote>"Collective Strength betyder att varje klient drar nytta av nÃ¤tverkets skala samtidigt som fullstÃ¤ndig individuell konfidentialitet bibehÃ¥lls."</blockquote>
<p>Kunder som trodde 0,65% upptÃ¤cker 1,30%. Genom Aureum: 0,60-0,80% allt inklusive. BerÃ¤kningen Ã¤r enkel. Men gÃ¶rs sÃ¤llan. Aureum gÃ¶r det.</p>`}
];

// ENGLISH ARTICLES
const ARTICLES_EN=[
{title:"Why Finland First?",
sub:"On being Finnish, serving Finns, and why this market matters more than its size suggests.",
date:"February 2026",
body:`<p>There's a question I get asked often, usually by investors from other markets: "Why focus on Finland? It's a small market. Why not start in London, Zurich, or Luxembourg?"</p>
<p>Fair question. And the answer is both simple and deeply personal.</p>
<p>Because I'm Finnish. And because Finland deserves better.</p>
<blockquote>"Home isn't just coordinates on a map. It's where your people are."</blockquote>
<p>I grew up between worldsâ€”born in the United States, childhood years in JyvÃ¤skylÃ¤ and Helsinki, but most of my life in Luxembourg. But Finland was always home. Not because of where I was born geographically. Home is where the language feels natural in your mouth, not translated in your head. Where you don't have to explain the small thingsâ€”why you take your shoes off at the door, why silence in a sauna is sacred, why "kalsarikÃ¤nnit" is a perfectly reasonable way to spend a Friday.</p>
<p>Both my parents are Finnish. My extended family is spread across Helsinki, JyvÃ¤skylÃ¤, the United States, and Luxembourgâ€”truly international. Summer cottages on lakes whose names I can barely pronounce but whose water I've known since I was five. Conversations at kitchen tables that switch between Finnish and English mid-sentence because that's just how we talk.</p>
<p>My mother tongue is Finnish. I speak English, French, Luxembourgish, a bit of German and Spanish. But Finnish is the language I think in. Finnish is the language that feels like home.</p>
<p>When I decided to build Aureum, I could have started anywhere. Luxembourg, where I live. London, where the money is. Zurich, where the banks are.</p>
<p>But I started with Finland. Not because it's the biggest market. Because it's my market. My people.</p>
<p>And because after fifteen years of watching Finnish investors get a raw deal, I'd had enough.</p>
<blockquote>"You're paying some of the highest private banking fees in Europe."</blockquote>
<p>Here's something most Finns don't realize: you're paying some of the highest private banking fees in Europe. Not because Finnish banks are greedy. They're not. They're solid, well-run institutions. But because the market is small. And when the market is small, there's less competition.</p>
<p>A â‚¬2M portfolio in Finland might pay 1.2-1.5% in total costs when you include all the layersâ€”management fees, fund costs, custody, FX spreads, transaction charges. That same portfolio in Luxembourg? 0.7-0.9% all-in. In London or Zurich? Similar. Sometimes even lower, especially above â‚¬5M.</p>
<p>The difference isn't the service quality. Finnish banks provide excellent service. The people are professionals. The structures are sound. The difference is market dynamics.</p>
<p>Luxembourg has 140+ banks competing for private banking clients. London has even more. Zurich is one of the world's deepest wealth management centers. Competition drives innovation. It drives transparency. It drives pricing down.</p>
<p>Finland has maybe five serious private banking players. That's it.</p>
<p>And when you're a â‚¬1M or â‚¬3M or even â‚¬10M client in Helsinki, you have limited leverage. The bank knows you probably don't speak German well enough to move to Credit Suisse. You probably don't want the complexity of opening accounts in three jurisdictions. You probably just want to work with someone local who speaks Finnish.</p>
<p>So the pricing stays high. Not exploitative. Just... high. And most Finns accept it because they don't know what the alternative looks like.</p>
<blockquote>"Access should not be a privilege."</blockquote>
<p>Here's what bothers me most: The wealthiest Finnsâ€”the ones with â‚¬20M, â‚¬50M, â‚¬100M+â€”they already have access to better pricing. They have advisors who negotiate on their behalf. They have family offices that maintain relationships with five banks across three countries. They get institutional pricing, better fund share classes, dedicated teams.</p>
<p>But if you're a successful entrepreneur in Tampere who just sold your company for â‚¬3M? You're on your own. If you're a doctor in Oulu with â‚¬800K in savings who wants to retire comfortably? You get retail pricing. You get generic fund recommendations.</p>
<p>That's not right. The knowledge that better pricing exists shouldn't be reserved for people who already have generational wealth. The ability to compare five bank proposals side by side shouldn't require hiring a consultant for â‚¬50,000.</p>
<p>Finland is full of smart, successful people who've built real wealth through hard work. Tech founders. Business owners. Medical professionals. Investors who made good decisions over decades. They deserve the same access to competitive banking that someone in Geneva gets automatically.</p>
<p>That's what Aureum is for.</p>
<blockquote>"In a small market, word spreads fast."</blockquote>
<p>Finland has about 5.5 million people. Of those, maybe 50,000-100,000 have meaningful investable wealthâ€”say, â‚¬250K and up. That's a tiny market compared to the UK, Germany, or France.</p>
<p>But it's also a perfect place to start. Because in a small market, word spreads fast. In Finland, everyone knows someone who knows someone. If Aureum helps one client in Helsinki save â‚¬15,000 a year in fees and get better reporting, that person tells their brother-in-law. Who tells his business partner. Who mentions it at a sauna evening with three other entrepreneurs.</p>
<p>Within six months, half the private banking clients in Southern Finland have heard about us. That's the advantage of a small, connected market. Trust is built through networks. Reputation matters more than marketing.</p>
<p>And frankly? I'd rather build something meaningful in Finland than build something big somewhere else. If Aureum helps 500 Finnish families get better banking over the next three years, that matters to me more than managing â‚¬5 billion in assets for clients I'll never meet.</p>
<p>This isn't philanthropy. It's personal.</p>
<blockquote>"You don't want to discuss inheritance in your third language."</blockquote>
<p>There's another reason Finland makes sense: we understand the culture. Finnish investors are, on average, more financially conservative than investors in some other markets. That's not a criticismâ€”it's a strength. Finns don't chase returns recklessly. They value stability. They plan for the long term. They don't trust flashy promises.</p>
<p>They also don't like to complain. If a Finnish client is unhappy with their bank, they're more likely to quietly suffer for five years than to call and make demands. That's just the culture. "En viitsi vaivata" â€” I don't want to bother anyone.</p>
<p>That's exactly the kind of client who benefits most from Aureum. Because we do the bothering for you. We ask the uncomfortable questions. We request the fee breakdowns. We compare the proposals. We negotiate. You don't have to be pushy. You just have to say yes to better terms when we bring them to you.</p>
<p>And then there's language. When you're discussing your children's inheritance, or your retirement plan, or how to structure â‚¬5M to minimize wealth tax across two generationsâ€”you don't want to do that in your third language. You want to do it in Finnish. Or Swedish.</p>
<p>Most international private banks will find you someone who speaks "some Finnish." That's not the same. Aureum finds you Finnish-speaking bankers at international banks. People who are Finnish, or who grew up in Finland, or who've worked with Finnish families for twenty years. People who understand that when a Finnish client says "ehkÃ¤" it might mean no.</p>
<p>Language isn't just words. It's trust.</p>
<blockquote>"Finland first. Then the Nordics. Then beyond."</blockquote>
<p>So yesâ€”we started with Finland. But the plan was never to stop there. The same dynamics that make Finland underserved apply to Estonia, Latvia, Lithuania. They apply to parts of Sweden outside Stockholm. They apply to Norway outside Oslo.</p>
<p>Small markets. High local pricing. Limited competition. Investors who deserve better but don't know how to access it.</p>
<p>Once we've proven the model works in Finlandâ€”once we've helped a few hundred families get better banking, lower costs, and real transparencyâ€”we'll expand. Swedish-speaking clients in Vaasa will tell their cousins in Stockholm. Estonian entrepreneurs in Tallinn will hear about us through Finnish business partners.</p>
<p>But we start here. At home. With our people. Because this isn't just a business. It's a correction.</p>
<p>For too long, Finnish investors have accepted high fees and limited options as just "how things are." For too long, access to global private banking has been reserved for people who already had connections in Zurich or Geneva.</p>
<p>That era is over. Aureum exists to level that playing field. To bring institutional-quality banking oversight to anyone with â‚¬250,000 or more. To make sure that a successful entrepreneur in JyvÃ¤skylÃ¤ gets the same pricing transparency as a billionaire in Monaco.</p>
<p>Not because it's profitable. Not because it's easy. Because it's right. And because Finlandâ€”my Finlandâ€”deserves it.</p>
<p><em>Kotona on siellÃ¤, missÃ¤ sydÃ¤n on. Ja minun sydÃ¤meni on Suomessa.</em></p>
<p><em>Home is where the heart is. And my heart is in Finland.</em></p>`},

{title:"Why Aureum Is a Technology Company â€” Not an Investment Company",
sub:"Understanding wealth from both sides: private banking heritage meets modern technology infrastructure.",
date:"February 2026",
body:`<p>I remember the exact moment I realized what was wrong.</p>
<p>I was sitting at a family dinner in Luxembourg. My fatherâ€”who'd spent nearly twenty years advising some of Finland's wealthiest families from his desk at a Swiss private bankâ€”had just won a significant new client mandate. A successful technology entrepreneur with a â‚¬3M portfolio.</p>
<p>The entrepreneur had been with another major European bank for eight years. When my father presented his proposal, he did something simple: he showed the client a single-page breakdown of total costs. Management fee, custody, transaction costs, FX spreadsâ€”everything, clearly laid out.</p>
<p>The competing bank had quoted "0.65% management fee." My father's analysis showed the client was actually paying 1.45% in total costs when you included all the hidden layers.</p>
<p>My father's all-in proposal? 0.85%. Higher management fee, but transparent. Everything included. No surprises.</p>
<p>The client switched within two weeks.</p>
<p>"They never showed me the full picture," the client said. "You did."</p>
<p>And I remember thinking: <em>That shouldn't be a competitive advantage. That should be standard.</em></p>
<blockquote>"The gap wasn't about intelligence or sophistication. It was about infrastructure."</blockquote>
<p>I grew up in a strange intersection. On one side: Swiss private banking. Relationship-driven, discreet, built on trust that spans generations. On the other: institutional private equity, where my mother's career was all about governance frameworks and mandate discipline. Every basis point mattered. Every manager was benchmarked.</p>
<p>I saw the same wealthâ€”often managed by the same institutionsâ€”treated completely differently depending on which side of that line you sat on. Institutional investors had dashboards, data, and accountability. Private investors had quarterly PDFs and trust.</p>
<p>Here's what I learned watching this industry for two decades: Private banking has world-class professionals and excellent products. But the <em>systems</em>â€”the technology that's supposed to make all of this transparent and efficientâ€”are shockingly outdated.</p>
<p>Clients are expected to make some of the most important financial decisions of their lives based on scattered reports from multiple banks, fee structures that require a forensic accountant to decode, and information that arrives weeks after it matters.</p>
<blockquote>"That's not a people problem. That's a technology problem."</blockquote>
<p>Aureum Private Office doesn't compete with banks. We don't manage money. We don't sell products. We built something different: a technology-driven platform that sits <em>above</em> banks and wealth managers.</p>
<p>Think of us as the operating system for your wealth. Your banks are the apps. We aggregate information across institutions, standardize fragmented reports, surface every cost layer clearly, run institutional-grade analysis, and give you a clean, real-time view of your entire wealth picture.</p>
<p>Here's the advantage of being a technology company instead of a bank: We're not stuck with systems built in the 1990s. We're not protecting legacy revenue streams. We're not constrained by what "the industry has always done."</p>
<p>So we use the best analytics tools available, institutional risk models that were previously reserved for billion-dollar portfolios, and modern communication channels. When a client asks a question, the answer shouldn't depend on which bank they're using or which reporting format happens to exist. Technology lets us unify that view.</p>
<blockquote>"Modern wealth doesn't move on a quarterly reporting cycle."</blockquote>
<p>At Aureum, clients have on-demand access to insightsâ€”delivered directly through secure channels, when it actually matters. Not noise. Not headlines. Relevant, timely context. Technology enables that immediacy. Judgment ensures it's actually useful.</p>
<p>I learned early on that technology without understanding wealth is dangerous. But wealth management without technology is just inefficient. What makes Aureum different is that we understand both worldsâ€”fluently.</p>
<p>We understand how private banks actually price, where the real costs hide, and how negotiations work. And we understand how modern platforms scale, how data should flow, and how to build tools that people actually use.</p>
<blockquote>"Our incentives are refreshingly simple: We don't earn commissions. We don't benefit when costs are opaque. We don't profit from complexity."</blockquote>
<p>Our fee is transparent: 0.05%-0.15% annually for oversight (tiered by portfolio size), plus 10% of documented cost savings. When we reduce your costs, we participate. Technology is what makes that alignment possible at scale.</p>
<p>Private wealth doesn't need more funds or investment strategies. It needs better infrastructure. Better information. Better tools. Better visibility. That's what we built. Not another investment firm promising returns. Not another advisor selling solutions. A technology platform that makes wealth oversight transparent, accessible, and independent.</p>
<p>Because in 2026, your wealth deserves better infrastructure than scattered PDFs and phone calls. It deserves what institutional investors have had for decades: clarity, data, and accountability.</p>
<p>That's Aureum Private Office. And that's why we're a technology company.</p>`},

{title:"The Discipline of Structural Comparison",
sub:"Why oversight, not performance, determines long-term outcomes in private wealth.",
date:"February 2026",
body:`<p>In private wealth, performance attracts attention. Structure rarely does.</p>
<p>Markets move. Strategies rotate. Headlines change. Yet over extended periods, what shapes outcomes most predictably is not volatility, but architecture: custody arrangements, fee layers, platform design, execution quality, and governance.</p>
<p>It was this distinction that led to the founding of Aureum.</p>
<p>Institutional investors benchmark systematically. They renegotiate custody agreements. They quantify total cost layers. They reassess structures as conditions evolve. Review is embedded into the system.</p>
<p>Private investors, by contrast, often maintain long-standing banking relationships that go structurally unexamined for years. Not because they lack expertise, but because comparison is rarely institutionalised in private wealth.</p>
<p>Over time, the effect compounds quietly.</p>
<blockquote>\u201CReturns are probabilistic. Costs are mathematical.\u201D</blockquote>
<p>A marginal structural inefficiency \u2014 whether in custody pricing, embedded platform fees, execution spreads, or product architecture \u2014 may appear immaterial in isolation. Over a decade or more, it is not.</p>
<p>Yet many investors cannot clearly quantify their total effective cost of ownership across all layers of their banking relationship. Nor can they easily assess whether their structure remains competitive relative to alternatives in the market.</p>
<p>Aureum was established to address precisely that gap.</p>
<p>The firm does not provide investment advice. It does not distribute products. It does not represent banks. Instead, it focuses exclusively on independent structural analysis and comparative benchmarking. Existing arrangements are reviewed, cost layers are consolidated and quantified, and alternatives are evaluated against measurable criteria.</p>
<blockquote>\u201COur role is analytical. We are not here to replace banks. We are here to introduce disciplined comparison.\u201D</blockquote>
<p>Historically, such oversight was typically associated with family offices or institutional investors with sufficient scale to justify internal review processes. Aureum\u2019s argument is that technological infrastructure has changed that equation. Consolidated reporting systems, cross-platform benchmarking tools, and structured cost analysis now allow independent comparison to be delivered efficiently and without institutional overhead.</p>
<p>The firm serves investors with meaningful capital \u2014 in practice, typically from \u20AC250,000 and above. Below that threshold, structural differences may not justify formal analysis. Above it, they often do.</p>
<p>The principle, however, scales. A \u20AC400,000 portfolio and a \u20AC40 million structure both benefit from disciplined benchmarking. The magnitude differs; the logic does not.</p>
<blockquote>\u201COversight is not a function of wealth tier. It is a function of seriousness.\u201D</blockquote>
<p>Importantly, Aureum\u2019s positioning is not limited to international clients. While Luxembourg provides proximity to one of Europe\u2019s principal financial centres, the need for structural clarity is not geographic. Domestic investors face the same fee layers, platform decisions, and custody considerations as cross-border clients.</p>
<p>Private banking is relationship-driven. That is not inherently a flaw. But trust and verification should coexist. Comparison should not be exceptional. It should be routine.</p>
<p>The firm\u2019s philosophy is deliberately restrained. It does not promise outperformance. It does not claim predictive advantage.</p>
<p>Better returns cannot be guaranteed. Lower unnecessary costs can be identified. Structural alignment can be verified.</p>
<p>In a market where innovation is often equated with disruption, the approach is more measured.</p>
<blockquote>\u201CPrivate wealth does not need disruption. It needs structure.\u201D</blockquote>
<p>And structure, unlike markets, can be examined.</p>`},

{title:"Age, Trust, and the Architecture of Oversight",
sub:"Why structural alignment matters more than tenure in modern wealth management.",
date:"February 2026",
body:`<p>\u201CYou\u2019re relatively young. Why should serious investors trust you?\u201D</p>
<p>It is a fair question. Trust in wealth management has historically been associated with age \u2014 grey hair, long tenure, established relationships. These signals carry weight. They should.</p>
<p>But Aureum is not built on relationship tenure. It is built on structural analysis.</p>
<blockquote>\u201CI am not asking investors to trust my market predictions. I am asking them to examine measurable structures.\u201D</blockquote>
<p>Aureum does not provide investment advice. It does not select securities. It does not compete with portfolio managers. Its role is analytical: consolidating cost layers, benchmarking custody arrangements, comparing platforms, and quantifying structural efficiency across jurisdictions.</p>
<p>That work does not depend on age. It depends on precision.</p>
<p>Noah Kraama\u2019s exposure to private banking began early. His father spent nearly two decades at one of Switzerland\u2019s most established private banking institutions, advising some of Finland\u2019s wealthiest families from Luxembourg. His mother built her career in institutional private equity, where governance frameworks and mandate discipline are foundational. The contrast between these two worlds \u2014 one relationship-driven, the other systematically reviewed \u2014 shaped his understanding of where private wealth falls short.</p>
<p>But the defining advantage is technological fluency.</p>
<blockquote>\u201CWe are building infrastructure. This is not a traditional advisory firm. It is a technology-enabled oversight layer.\u201D</blockquote>
<p>Modern benchmarking, automated cost aggregation, cross-platform comparison, and structured multilingual reporting require system design. They require comfort with data architecture. They require a native understanding of how analytical tools scale \u2014 from a single portfolio to hundreds.</p>
<p>That generational fluency is not cosmetic. It is functional.</p>
<p>Large institutional investors already operate with consultants, data systems, and systematic review frameworks. Private investors, until recently, did not have efficient access to that discipline. Technology now makes it possible. Aureum exists at that intersection: institutional logic, delivered through modern infrastructure.</p>
<blockquote>\u201CWe do not sell products. We do not earn retrocessions. We do not represent banks. Our incentives are structural.\u201D</blockquote>
<p>Trust, ultimately, should not be anchored to age alone. It should be anchored to alignment and transparency. The question is not how long someone has been in the room. It is whether the system they build introduces measurable clarity.</p>
<p>Experience matters. But so does modernisation. The future of oversight will be data-driven \u2014 and Aureum was built native to that environment.</p>
<p>For investors with meaningful capital, the standard is simple: does the structure stand up to scrutiny? If it does, age is irrelevant. If it does not, tenure will not compensate for it.</p>`},

{title:"The Language Gap in International Banking",
sub:"Why your banker\u2019s language matters more than their bank\u2019s brand.",
date:"February 2026",
body:`<p>There is a particular kind of meeting that happens thousands of times each year across the private banking world. A Finnish entrepreneur sits across from a relationship manager in Geneva or Luxembourg. The banker speaks English fluently \u2014 sometimes French, sometimes German. The conversation is professional. The presentations are polished. And yet something essential is lost.</p>
<p>Wealth is not an abstract subject. It carries the weight of family history, of generational planning, of anxieties that do not translate easily across cultural boundaries. The decision to move capital across borders is not purely financial. It is personal.</p>
<blockquote>\u201CDiscussing your children\u2019s inheritance in your third language is not the same as discussing it in your first.\u201D</blockquote>
<p>This is a gap that rarely appears in pitch decks or bank brochures. Private banks compete on brand, on AUM thresholds, on product offerings, on performance track records. They do not typically compete on whether their relationship manager can discuss estate planning in Finnish over coffee.</p>
<p>Yet from the client\u2019s perspective, language is often the single most important factor in whether a banking relationship feels like oversight or like partnership.</p>
<p>The Nordic market illustrates this clearly. Finland and Sweden produce a disproportionate number of internationally mobile entrepreneurs and investors \u2014 people whose wealth has outgrown domestic banking infrastructure but whose cultural identity remains firmly Nordic. They want international capability. They also want to be understood.</p>
<p>These two things are not as easy to combine as one might expect.</p>
<p>There are Finnish-speaking bankers at international institutions. There are Swedish-speaking private bankers in Luxembourg, in Geneva, in Singapore. But finding them requires knowing where to look \u2014 and most investors do not. The information is not published. It is not searchable. It exists within networks, within referrals, within decades of relationship-building that most private clients have no access to.</p>
<blockquote>\u201CThe best banker for you might be in a city you have never considered, speaking the language you grew up with.\u201D</blockquote>
<p>This is one of Aureum\u2019s foundational principles. When we source proposals from our network of 25+ banks, language matching is not an afterthought. It is the first filter. Before fee structures, before product platforms, before investment philosophy \u2014 we ask: can this banker conduct business in the language the client thinks in?</p>
<p>The results are often surprising. A Finnish entrepreneur based in London, who had assumed their only option was an English-speaking banker, discovers a Finnish-speaking relationship manager at a top-tier Swiss bank in Luxembourg who also understands Nordic tax structures. A Vaasa-based family office finds a Swedish-speaking team in Singapore that specialises in exactly their asset class.</p>
<p>These are not marginal improvements. They change the nature of the relationship entirely.</p>
<blockquote>\u201CTrust is built in the language you think in.\u201D</blockquote>
<p>Private banking has always been a relationship business. That is its greatest strength and its most persistent blind spot. The relationships that endure are not built on brand prestige or product innovation. They are built on understanding. And understanding begins with language.</p>
<p>Aureum does not believe this will change. It believes it should be easier to find.</p>`},

{title:"The Hidden Cost Layer",
sub:"Why your bank\u2019s quoted fee is only the beginning \u2014 and what Collective Strength changes.",
date:"February 2026",
body:`<p>Ask a Finnish private banking client what they pay in fees, and most will give you a single number. \u201C0.65%,\u201D they might say. Or \u201C0.70%.\u201D</p>
<p>That number is real. It appears on their fee schedule. Their bank discloses it transparently. And it is, almost always, incomplete.</p>
<p>The management fee is one layer. Beneath it sit several others \u2014 each individually modest, collectively significant, and rarely presented as a total.</p>
<blockquote>\u201CThe fee you see is not the fee you pay.\u201D</blockquote>
<p>A typical Nordic private banking relationship involves at least six distinct cost layers:</p>
<p><strong>Layer 1: Management fee.</strong> The headline number. Typically 0.50\u20130.70% for a discretionary mandate. This is what the bank quotes, what the client remembers, and what appears in marketing materials.</p>
<p><strong>Layer 2: Foreign exchange costs \u2014 the single largest hidden fee.</strong> This is the one most clients never think to ask about, and the one banks are least eager to discuss. Every time your portfolio trades a non-base-currency security, the bank applies an FX spread. These spreads are not disclosed as fees. They do not appear on your fee schedule. They are embedded invisibly in the execution price. A typical private bank applies a spread of 0.30\u20131.00% on each currency conversion. For an internationally diversified portfolio with 40\u201360% in non-EUR assets, the annual cost can easily reach 0.20\u20130.50% of total AUM \u2014 every year, compounding silently. On a \u20AC2M portfolio, that is \u20AC4,000\u201310,000 per year that never appears on any statement. Banks earn billions from FX spreads precisely because clients do not see them.</p>
<p><strong>Layer 3: Underlying fund costs.</strong> If your portfolio contains mutual funds or ETFs, each carries its own expense ratio \u2014 typically 0.20\u20130.60% for actively managed funds. These fees are deducted inside the fund, invisible on your statement, but very real in their impact on returns. Nordic banks often use their own house funds, which carry higher costs than equivalent institutional share classes.</p>
<p><strong>Layer 4: Custody fee.</strong> The cost of holding your assets. Usually 0.05\u20130.15%, sometimes waived for larger portfolios, sometimes buried in the account terms. Many clients do not know this fee exists.</p>
<p><strong>Layer 5: Transaction costs.</strong> Every trade incurs a cost. Some banks charge explicit commissions; others embed the cost in wider bid-ask spreads. Estimated at 0.10\u20130.20% annually for a moderately active portfolio.</p>
<p><strong>Layer 6: Platform and account charges.</strong> Account maintenance, platform access fees, reporting charges, and minimum balance penalties. Individually small; collectively, they add 0.05\u20130.10%.</p>
<p>Sum these layers, and the client paying a \u201C0.65%\u201D management fee is often paying 1.20\u20131.80% in total effective cost. On a \u20AC2M portfolio over ten years, that hidden 0.60\u20131.15% costs approximately \u20AC120,000\u2013230,000 in lost compounding. The FX layer alone may account for a third of that loss.</p>
<blockquote>\u201CMost investors cannot quantify their total effective cost of ownership. That is not an accident.\u201D</blockquote>
<p>This is not a uniquely Finnish problem, but the Nordic market has a specific variant of it. Many domestic banks distribute primarily their own funds \u2014 house funds with higher expense ratios than equivalent institutional share classes available through international platforms. A Nordea balanced fund might carry an ongoing charge of 0.45%, while the institutional share class of a comparable Vanguard or BlackRock fund costs 0.08\u20130.15%. The performance difference is often negligible; the cost difference is not.</p>
<p>International private banks operate differently. Many offer all-in pricing \u2014 a single fee that covers management, custody, and transaction costs. Others provide access to institutional share classes that are simply unavailable through domestic retail platforms. The structural result is the same: lower total cost for equivalent or superior service.</p>
<blockquote>\u201CThe question is not whether your bank is good. The question is whether your structure is efficient.\u201D</blockquote>
<p>This is where Aureum\u2019s approach becomes relevant. When we analyse a client\u2019s existing arrangement, we do not stop at the management fee. We quantify every layer \u2014 disclosed, estimated, and hidden. We then present this total alongside proposals from competing banks, many of which offer structurally different pricing models.</p>
<p>But there is a second dimension that amplifies this advantage: collective negotiating power.</p>
<p>Aureum\u2019s Collective Strength programme presents individual mandates to banks as part of a larger pool of Nordic investor AUM. Each client maintains entirely separate, individual accounts. No assets are commingled. But from the bank\u2019s perspective, the relationship represents significant aggregate volume \u2014 and banks price accordingly.</p>
<p>A \u20AC1M individual mandate receives standard pricing. A \u20AC1M mandate presented as part of \u20AC25M of Nordic AUM receives institutional attention. Better fee schedules. Access to share classes normally reserved for larger clients. Priority onboarding. Dedicated relationship management.</p>
<blockquote>\u201CCollective Strength means every client benefits from the scale of the network, while maintaining complete individual confidentiality.\u201D</blockquote>
<p>The combination of fee layer transparency and collective negotiating power produces measurable results. Clients who assumed they were paying 0.65% discover they were paying 1.30%. The same clients, through Aureum\u2019s sourcing, receive proposals at 0.60\u20130.80% all-in \u2014 with better fund access, multilingual service, and independent reporting included.</p>
<p>The arithmetic is not complex. But it is rarely done. Aureum exists to do it.</p>`}
];


/* â•â•â• v15: LOGO SVG â€” Option 3 (Structural A + Diamond Cap) â•â•â• */
const Logo=({size=28,color="currentColor",showText=false,subtitle="PRIVATE OFFICE"})=>(
  <svg viewBox="0 0 32 38" width={size} height={size*38/32} fill="none">
    <defs><linearGradient id="lgAu" x1="0%" y1="0%" x2="0%" y2="100%"><stop offset="0%" style={{stopColor:"#D4A853"}}/><stop offset="100%" style={{stopColor:"#B8863F"}}/></linearGradient></defs>
    <line x1="4" y1="36" x2="16" y2="2" stroke="url(#lgAu)" strokeWidth="2.2" strokeLinecap="round"/>
    <line x1="28" y1="36" x2="16" y2="2" stroke="url(#lgAu)" strokeWidth="2.2" strokeLinecap="round"/>
    <polygon points="16,16 22,20 16,24 10,20" fill="none" stroke="url(#lgAu)" strokeWidth="1.2"/>
    <polygon points="16,2 20,6 16,10 12,6" fill="url(#lgAu)"/>
  </svg>
);

/* â•â•â• ICONS â•â•â• */
const Lock=({s=14})=><svg width={s} height={s} viewBox="0 0 14 14" fill="none"><rect x="2" y="6" width="10" height="7" rx="1.5" stroke="currentColor" strokeWidth="1.2"/><path d="M4.5 6V4.5a2.5 2.5 0 015 0V6" stroke="currentColor" strokeWidth="1.2"/></svg>;
const Arr=()=><svg width="15" height="15" viewBox="0 0 16 16" fill="none"><path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" strokeWidth="1.3"/></svg>;
const Burger=({open})=><svg width="20" height="20" viewBox="0 0 20 20" fill="none"><path d={open?"M5 5l10 10M15 5L5 15":"M3 6h14M3 10h14M3 14h14"} stroke="currentColor" strokeWidth="1.5" strokeLinecap="round"/></svg>;

/* â•â•â• v13: HERO BACKGROUND â•â•â• */
function HeroBG(){
  return(
    <div className="hero-bg">
      <div className="hero-grid"/>
      <div className="hero-glow hero-glow-1"/>
      <div className="hero-glow hero-glow-2"/>
      {[...Array(6)].map((_,i)=><div key={i} className={`hero-diamond hd-${i}`}/>)}
      <div className="hero-line hero-line-1"/>
      <div className="hero-line hero-line-2"/>
      <div className="hero-line hero-line-3"/>
    </div>
  );
}

/* â•â•â• v13: FAQ ACCORDION â•â•â• */
/* â•â•â• v26: HERO STAT COUNTER â•â•â• */
function CountStat({num,suffix,prefix,label}){
  const[count,setCount]=useState(0);
  const[started,setStarted]=useState(false);
  const ref=useRef(null);
  useEffect(()=>{
    const el=ref.current;if(!el)return;
    const io=new IntersectionObserver(([e])=>{if(e.isIntersecting&&!started){setStarted(true);io.disconnect()}},{threshold:0.5});
    io.observe(el);return()=>io.disconnect();
  },[started]);
  useEffect(()=>{
    if(!started)return;
    if(num===0){setCount(0);return}
    const dur=1200;const steps=40;const inc=num/steps;
    let frame=0;
    const iv=setInterval(()=>{frame++;setCount(Math.min(Math.round(inc*frame),num));if(frame>=steps)clearInterval(iv)},dur/steps);
    return()=>clearInterval(iv);
  },[started,num]);
  return <div ref={ref} className="hero-stat"><div className="hero-stat-n">{prefix||""}{count}{suffix||""}</div><div className="hero-stat-l">{label}</div></div>;
}

function FAQ({t}){
  const[open,setOpen]=useState(null);
  return(
    <div className="faq-list">
      {t.faqs.map((f,i)=>(
        <div key={i} className={"faq-item"+(open===i?" open":"")}>
          <button className="faq-q" onClick={()=>setOpen(open===i?null:i)}>
            <span>{f[0]}</span>
            <span className="faq-icon">{open===i?"\u2212":"+"}</span>
          </button>
          <div className="faq-a"><div className="faq-a-in">{f[1]}</div></div>
        </div>
      ))}
    </div>
  );
}

/* â•â•â• v13: SOCIAL PROOF â•â•â• */
function SocialProof({t}){
  return(
    <div className="sp">
      <p className="sp-intro">{t.sp_intro}</p>
      <div className="sp-timeline">
        {t.sp_steps.map((s,i)=>(
          <div key={i} className="sp-step">
            <div className="sp-marker"><span className="sp-icon">{s[2]}</span></div>
            <div className="sp-content">
              <div className="sp-day">{s[0]}</div>
              <div className="sp-desc">{s[1]}</div>
            </div>
          </div>
        ))}
      </div>
      <div className="sp-results">
        {t.sp_results.map((r,i)=>(
          <div key={i} className="sp-stat">
            <div className="sp-stat-v">{r[0]}</div>
            <div className="sp-stat-l">{r[1]}</div>
          </div>
        ))}
      </div>
      <div className="sp-note">{t.sp_note}</div>
    </div>
  );
}

/* â•â•â• KYC â€” v35: Natural onboarding with checkpoint & investment profile â•â•â• */
const KYC_STEPS={
en:[
  // Phase 1: Basics
  {msg:"Welcome to Aureum. This secure conversation takes just a few minutes. Your information is encrypted and never shared without your consent.",qr:["Let's begin"],phase:"welcome",prog:0},
  {msg:"What's your full name?",field:"firstName",type:"text",ph:"Full name",phase:"personal",prog:8},
  {msg:"What's your nationality?",field:"nationality",type:"text",ph:"e.g. Finnish",phase:"personal",prog:16},
  {msg:"Where do you currently live?",field:"residence",type:"text",ph:"Country of residence",phase:"personal",prog:24},
  {msg:"What do you do? And what's the primary source of your wealth?",field:"occupation",type:"text",ph:"e.g. Tech entrepreneur, business sale",phase:"personal",prog:32},
  {msg:"What's your approximate investable wealth? This helps us match you with the right banks and jurisdictions.",field:"totalInvestable",type:"select",opts:["â‚¬250K â€“ â‚¬1M","â‚¬1M â€“ â‚¬3M","â‚¬3M â€“ â‚¬5M","â‚¬5M â€“ â‚¬15M","â‚¬15M+"],phase:"financial",prog:40},
  {msg:"Which banks do you currently work with, if any?",field:"currentBanks",type:"text",ph:"e.g. Nordea, OP, or none currently",phase:"financial",prog:48},
  
  // Checkpoint
  {msg:"Perfect. I can continue asking a few more questions to understand your investment approach betterâ€”this helps us find the perfect banking match. Or, if you prefer, I can connect you directly with Noah via email to finish this conversation personally. What works better for you?",type:"checkpoint",opts:["Continue here (3 more minutes)","Finish via email with Noah"],phase:"checkpoint",prog:54},
  
  // Phase 2: Service Model & Investment Profile (if they continue)
  {msg:"Great. Let's talk about your investment approach. Most clients fall into one of two categories: **Discretionary** â€” you trust your banker to make investment decisions within agreed parameters, or **Advisory** â€” your banker provides recommendations but you make the final calls. Which resonates more with you?",field:"serviceModel",type:"select",opts:["Discretionary (banker decides)","Advisory (I decide)","Not sure â€” help me choose"],phase:"investment",prog:60,explainer:"Discretionary means your banker manages your portfolio actively within risk limits you set. Advisory means you approve each trade. Most of our clients with â‚¬1Mâ€“5M prefer advisory. Above â‚¬5M, about 60% choose discretionary."},
  {msg:"What kind of returns are you targeting? Be honestâ€”there's no wrong answer.",field:"returnExpectation",type:"select",opts:["Conservative (3-5% annually)","Balanced (5-8% annually)","Growth-focused (8%+ annually)"],phase:"investment",prog:68},
  {msg:"How comfortable are you with portfolio volatility? In other words, could you stomach seeing your portfolio drop 15-20% in a bad year?",field:"riskTolerance",type:"select",opts:["Low â€” I prefer stability","Medium â€” I can handle some swings","High â€” I'm comfortable with volatility"],phase:"investment",prog:76},
  {msg:"What's your investment time horizon? When might you need to access a significant portion of this wealth?",field:"timeHorizon",type:"select",opts:["Short-term (under 3 years)","Medium-term (3-10 years)","Long-term (10+ years)"],phase:"investment",prog:84},
  
  // Option to continue or finish with Noah
  {msg:"Excellent. A few more quick questions help us narrow down the perfect banks for you. Want to continue here, or would you prefer to finish the rest with Noah via email?",type:"checkpoint2",opts:["Keep going (2 minutes)","Email Noah"],phase:"checkpoint2",prog:88},
  
  // Phase 3: Additional Details (if they continue)
  {msg:"Do you have any ESG or sustainability preferences for your investments?",field:"esgPreference",type:"select",opts:["Yes â€” this is important to me","Somewhat â€” nice to have","No preference"],phase:"details",prog:90},
  {msg:"How much liquidity do you need? In other words, how quickly might you need to access your capital?",field:"liquidityNeeds",type:"select",opts:["High â€” I need quick access","Medium â€” 1-2 weeks is fine","Low â€” I'm investing long-term"],phase:"details",prog:92},
  {msg:"Any specific investment restrictions or preferences? Certain sectors to avoid, geographies to exclude, etc.",field:"restrictions",type:"text",ph:"e.g. No tobacco, no crypto, or none",phase:"details",prog:94},
  
  // Phase 4: Preferences
  {msg:"Almost done. Which jurisdictions interest you for your banking? We'll recommend based on your profile, but your preferences help.",field:"jurisdictions",type:"multi",opts:["Finland","Luxembourg","Switzerland","United Kingdom","Singapore","UAE","Monaco","No preference â€” advise me"],phase:"preferences",prog:96},
  {msg:"Are you interested in an insurance wrapper (Luxembourg, Ireland, or Finland) for tax efficiency?",field:"insuranceWrapper",type:"select",opts:["Yes, interested","Not sure â€” tell me more","No, not needed"],phase:"preferences",prog:97},
  {msg:"What language should your banker speak?",field:"bankerLanguage",type:"select",opts:["Finnish","Swedish","English","No preference"],phase:"preferences",prog:98},
  {msg:"In which language would you like your reports?",field:"reportLanguage",type:"select",opts:["Finnish","Swedish","English"],phase:"preferences",prog:99},
  {msg:"Last question. What email should we use?",field:"email",type:"text",ph:"your@email.com",phase:"preferences",prog:100},
],
fi:[
  // Vaihe 1: Perustiedot
  {msg:"Tervetuloa Aureumiin. TÃ¤mÃ¤ turvallinen keskustelu kestÃ¤Ã¤ vain muutaman minuutin. Tietosi ovat salattuja eikÃ¤ niitÃ¤ koskaan jaeta ilman suostumustasi.",qr:["Aloitetaan"],phase:"welcome",prog:0},
  {msg:"MikÃ¤ on nimesi?",field:"firstName",type:"text",ph:"Koko nimi",phase:"personal",prog:8},
  {msg:"MikÃ¤ on kansalaisuutesi?",field:"nationality",type:"text",ph:"esim. Suomalainen",phase:"personal",prog:16},
  {msg:"MissÃ¤ asut tÃ¤llÃ¤ hetkellÃ¤?",field:"residence",type:"text",ph:"Asuinmaa",phase:"personal",prog:24},
  {msg:"MitÃ¤ teet tyÃ¶ksesi? Ja mikÃ¤ on varallisuutesi pÃ¤Ã¤asiallinen lÃ¤hde?",field:"occupation",type:"text",ph:"esim. TeknologiayrittÃ¤jÃ¤, yrityskauppa",phase:"personal",prog:32},
  {msg:"MikÃ¤ on arvioitu sijoitettava varallisuutesi? TÃ¤mÃ¤ auttaa meitÃ¤ yhdistÃ¤mÃ¤Ã¤n sinut oikeisiin pankkeihin.",field:"totalInvestable",type:"select",opts:["â‚¬250K â€“ â‚¬1M","â‚¬1M â€“ â‚¬3M","â‚¬3M â€“ â‚¬5M","â‚¬5M â€“ â‚¬15M","â‚¬15M+"],phase:"financial",prog:40},
  {msg:"MitÃ¤ pankkeja kÃ¤ytÃ¤t tÃ¤llÃ¤ hetkellÃ¤?",field:"currentBanks",type:"text",ph:"esim. Nordea, OP, tai ei pankkia",phase:"financial",prog:48},
  
  // Tarkistuspiste
  {msg:"Hienoa. Voin jatkaa muutamalla lisÃ¤kysymyksellÃ¤ ymmÃ¤rtÃ¤Ã¤kseni sijoituslÃ¤hestymistapasi paremminâ€”tÃ¤mÃ¤ auttaa lÃ¶ytÃ¤mÃ¤Ã¤n tÃ¤ydellisen pankin. Tai voit halutessasi jatkaa Noahin kanssa sÃ¤hkÃ¶postitse. Kumpi sopii paremmin?",type:"checkpoint",opts:["Jatka tÃ¤ssÃ¤ (3 minuuttia)","Jatka sÃ¤hkÃ¶postitse Noahin kanssa"],phase:"checkpoint",prog:54},
  
  // Vaihe 2: Palvelumalli ja sijoitusprofiili
  {msg:"Mainiota. Keskustellaan sijoituslÃ¤hestymistavastasi. Useimmat asiakkaat kuuluvat kahteen kategoriaan: **Diskretionaarinen** â€” luotat pankkiiriin tekemÃ¤Ã¤n sijoituspÃ¤Ã¤tÃ¶kset sovittujen parametrien puitteissa, tai **Neuvontatyyppinen** â€” pankkiiri antaa suosituksia mutta sinÃ¤ teet lopulliset pÃ¤Ã¤tÃ¶kset. Kumpi resonoi kanssasi?",field:"serviceModel",type:"select",opts:["Diskretionaarinen (pankkiiri pÃ¤Ã¤ttÃ¤Ã¤)","Neuvontatyyppinen (minÃ¤ pÃ¤Ã¤tÃ¤n)","En ole varma â€” auta valitsemaan"],phase:"investment",prog:60},
  {msg:"Millaista tuottoa tavoittelet? Ole rehellinenâ€”ei ole vÃ¤Ã¤rÃ¤Ã¤ vastausta.",field:"returnExpectation",type:"select",opts:["Konservatiivinen (3-5% vuodessa)","Tasapainoinen (5-8% vuodessa)","Kasvuhakuinen (8%+ vuodessa)"],phase:"investment",prog:68},
  {msg:"Kuinka mukavaa salkun heilahtelut ovat sinulle? Voisitko kestÃ¤Ã¤ nÃ¤hdÃ¤ salkkusi laskevan 15-20% huonona vuotena?",field:"riskTolerance",type:"select",opts:["Matala â€” pidÃ¤n vakautta","Keskitaso â€” kestÃ¤n jonkin verran heilahtelua","Korkea â€” olen mukava volatiliteetin kanssa"],phase:"investment",prog:76},
  {msg:"MikÃ¤ on sijoitusaikahorisonttisi? Milloin saatat tarvita merkittÃ¤vÃ¤n osan tÃ¤stÃ¤ varallisuudesta?",field:"timeHorizon",type:"select",opts:["Lyhyt (alle 3 vuotta)","KeskipitkÃ¤ (3-10 vuotta)","PitkÃ¤ (10+ vuotta)"],phase:"investment",prog:84},
  
  // Toinen tarkistuspiste
  {msg:"Erinomaista. Muutama lisÃ¤kysymys auttaa meitÃ¤ rajaamaan tÃ¤ydelliset pankit sinulle. Haluatko jatkaa tÃ¤ssÃ¤ vai viimeistellÃ¤ Noahin kanssa sÃ¤hkÃ¶postitse?",type:"checkpoint2",opts:["Jatketaan (2 minuuttia)","SÃ¤hkÃ¶posti Noahille"],phase:"checkpoint2",prog:88},
  
  // Vaihe 3: LisÃ¤tiedot
  {msg:"Onko sinulla ESG- tai kestÃ¤vyysmieltymyksiÃ¤ sijoituksiisi?",field:"esgPreference",type:"select",opts:["KyllÃ¤ â€” tÃ¤mÃ¤ on tÃ¤rkeÃ¤Ã¤","Jossain mÃ¤Ã¤rin â€” mukava lisÃ¤","Ei mieltymyksiÃ¤"],phase:"details",prog:90},
  {msg:"Kuinka paljon likviditeettiÃ¤ tarvitset? Kuinka nopeasti saatat tarvita pÃ¤Ã¤syÃ¤ pÃ¤Ã¤omaasi?",field:"liquidityNeeds",type:"select",opts:["Korkea â€” tarvitsen nopean pÃ¤Ã¤syn","Keskitaso â€” 1-2 viikkoa on ok","Matala â€” sijoitan pitkÃ¤ksi aikaa"],phase:"details",prog:92},
  {msg:"Onko sinulla erityisiÃ¤ sijoitusrajoituksia tai mieltymyksiÃ¤? TiettyjÃ¤ sektoreita vÃ¤ltettÃ¤vÃ¤, maantieteellisiÃ¤ alueita poissulkea jne.",field:"restrictions",type:"text",ph:"esim. Ei tupakkaa, ei kryptoa, tai ei rajoituksia",phase:"details",prog:94},
  
  // Vaihe 4: Mieltymykset
  {msg:"Melkein valmista. MitkÃ¤ lainkÃ¤yttÃ¶alueet kiinnostavat pankkitoiminnassasi?",field:"jurisdictions",type:"multi",opts:["Suomi","Luxemburg","Sveitsi","Iso-Britannia","Singapore","Arabiemiirikunnat","Monaco","Ei preferenssiÃ¤ â€” neuvo minua"],phase:"preferences",prog:96},
  {msg:"Oletko kiinnostunut vakuutuskuoresta (Luxemburg, Irlanti tai Suomi) verotehostamiseen?",field:"insuranceWrapper",type:"select",opts:["KyllÃ¤, kiinnostaa","En ole varma â€” kerro lisÃ¤Ã¤","Ei, ei tarvetta"],phase:"preferences",prog:97},
  {msg:"MillÃ¤ kielellÃ¤ pankkiirisi tulisi puhua?",field:"bankerLanguage",type:"select",opts:["Suomi","Ruotsi","Englanti","Ei preferenssiÃ¤"],phase:"preferences",prog:98},
  {msg:"MillÃ¤ kielellÃ¤ haluat raporttisi?",field:"reportLanguage",type:"select",opts:["Suomi","Ruotsi","Englanti"],phase:"preferences",prog:99},
  {msg:"Viimeinen kysymys. Mihin sÃ¤hkÃ¶postiin otamme yhteyttÃ¤?",field:"email",type:"text",ph:"sinun@email.fi",phase:"preferences",prog:100},
],
sv:[
  // Fas 1: GrundlÃ¤ggande
  {msg:"VÃ¤lkommen till Aureum. Detta sÃ¤kra samtal tar bara nÃ¥gra minuter. Din information Ã¤r krypterad och delas aldrig utan ditt samtycke.",qr:["LÃ¥t oss bÃ¶rja"],phase:"welcome",prog:0},
  {msg:"Vad heter du?",field:"firstName",type:"text",ph:"FullstÃ¤ndigt namn",phase:"personal",prog:8},
  {msg:"Vilken nationalitet har du?",field:"nationality",type:"text",ph:"t.ex. Finsk",phase:"personal",prog:16},
  {msg:"Var bor du fÃ¶r nÃ¤rvarande?",field:"residence",type:"text",ph:"BosÃ¤ttningsland",phase:"personal",prog:24},
  {msg:"Vad gÃ¶r du? Och vad Ã¤r den primÃ¤ra kÃ¤llan till din fÃ¶rmÃ¶genhet?",field:"occupation",type:"text",ph:"t.ex. TeknikentreprenÃ¶r, fÃ¶retagsfÃ¶rsÃ¤ljning",phase:"personal",prog:32},
  {msg:"Vad Ã¤r din ungefÃ¤rliga investerbara fÃ¶rmÃ¶genhet? Detta hjÃ¤lper oss att matcha dig med rÃ¤tt banker.",field:"totalInvestable",type:"select",opts:["â‚¬250K â€“ â‚¬1M","â‚¬1M â€“ â‚¬3M","â‚¬3M â€“ â‚¬5M","â‚¬5M â€“ â‚¬15M","â‚¬15M+"],phase:"financial",prog:40},
  {msg:"Vilka banker arbetar du med fÃ¶r nÃ¤rvarande?",field:"currentBanks",type:"text",ph:"t.ex. Nordea, OP, eller ingen",phase:"financial",prog:48},
  
  // Kontrollpunkt
  {msg:"Perfekt. Jag kan fortsÃ¤tta med nÃ¥gra fler frÃ¥gor fÃ¶r att fÃ¶rstÃ¥ din investeringsansats bÃ¤ttreâ€”detta hjÃ¤lper oss hitta den perfekta banken. Eller, om du fÃ¶redrar, kan jag koppla dig direkt med Noah via e-post fÃ¶r att avsluta detta samtal personligt. Vad fungerar bÃ¤ttre fÃ¶r dig?",type:"checkpoint",opts:["FortsÃ¤tt hÃ¤r (3 minuter)","Avsluta via e-post med Noah"],phase:"checkpoint",prog:54},
  
  // Fas 2: Servicemodell och investeringsprofil
  {msg:"UtmÃ¤rkt. LÃ¥t oss prata om din investeringsansats. De flesta kunder faller i en av tvÃ¥ kategorier: **DiskretionÃ¤r** â€” du litar pÃ¥ din bankir att fatta investeringsbeslut inom Ã¶verenskomna parametrar, eller **RÃ¥dgivande** â€” din bankir ger rekommendationer men du fattar de slutliga besluten. Vilket resonerar mer med dig?",field:"serviceModel",type:"select",opts:["DiskretionÃ¤r (bankiren beslutar)","RÃ¥dgivande (jag beslutar)","Inte sÃ¤ker â€” hjÃ¤lp mig vÃ¤lja"],phase:"investment",prog:60},
  {msg:"Vilken typ av avkastning siktar du pÃ¥? Var Ã¤rligâ€”det finns inget fel svar.",field:"returnExpectation",type:"select",opts:["Konservativ (3-5% Ã¥rligen)","Balanserad (5-8% Ã¥rligen)","TillvÃ¤xtfokuserad (8%+ Ã¥rligen)"],phase:"investment",prog:68},
  {msg:"Hur bekvÃ¤m Ã¤r du med portfÃ¶ljvolatilitet? Kunde du hantera att se din portfÃ¶lj sjunka 15-20% under ett dÃ¥ligt Ã¥r?",field:"riskTolerance",type:"select",opts:["LÃ¥g â€” jag fÃ¶redrar stabilitet","Medium â€” jag klarar vissa svÃ¤ngningar","HÃ¶g â€” jag Ã¤r bekvÃ¤m med volatilitet"],phase:"investment",prog:76},
  {msg:"Vad Ã¤r din investeringshorisont? NÃ¤r kan du behÃ¶va tillgÃ¥ng till en betydande del av denna fÃ¶rmÃ¶genhet?",field:"timeHorizon",type:"select",opts:["Kort sikt (under 3 Ã¥r)","MedellÃ¥ng sikt (3-10 Ã¥r)","LÃ¥ng sikt (10+ Ã¥r)"],phase:"investment",prog:84},
  
  // Andra kontrollpunkten
  {msg:"UtmÃ¤rkt. NÃ¥gra fler snabba frÃ¥gor hjÃ¤lper oss att begrÃ¤nsa de perfekta bankerna fÃ¶r dig. Vill du fortsÃ¤tta hÃ¤r eller fÃ¶redrar du att slutfÃ¶ra resten med Noah via e-post?",type:"checkpoint2",opts:["FortsÃ¤tt (2 minuter)","E-posta Noah"],phase:"checkpoint2",prog:88},
  
  // Fas 3: Ytterligare detaljer
  {msg:"Har du nÃ¥gra ESG- eller hÃ¥llbarhetspreferenser fÃ¶r dina investeringar?",field:"esgPreference",type:"select",opts:["Ja â€” detta Ã¤r viktigt fÃ¶r mig","NÃ¥got â€” trevligt att ha","Ingen preferens"],phase:"details",prog:90},
  {msg:"Hur mycket likviditet behÃ¶ver du? Hur snabbt kan du behÃ¶va tillgÃ¥ng till ditt kapital?",field:"liquidityNeeds",type:"select",opts:["HÃ¶g â€” jag behÃ¶ver snabb Ã¥tkomst","Medium â€” 1-2 veckor Ã¤r okej","LÃ¥g â€” jag investerar lÃ¥ngsiktigt"],phase:"details",prog:92},
  {msg:"NÃ¥gra specifika investeringsrestriktioner eller preferenser? Vissa sektorer att undvika, geografier att exkludera, etc.",field:"restrictions",type:"text",ph:"t.ex. Ingen tobak, ingen krypto, eller inga",phase:"details",prog:94},
  
  // Fas 4: Preferenser
  {msg:"NÃ¤stan klart. Vilka jurisdiktioner intresserar dig fÃ¶r din bankverksamhet?",field:"jurisdictions",type:"multi",opts:["Finland","Luxemburg","Schweiz","Storbritannien","Singapore","FÃ¶renade Arabemiraten","Monaco","Ingen preferens â€” rÃ¥dge mig"],phase:"preferences",prog:96},
  {msg:"Ã„r du intresserad av ett fÃ¶rsÃ¤kringsomslag (Luxemburg, Irland eller Finland) fÃ¶r skatteeffektivitet?",field:"insuranceWrapper",type:"select",opts:["Ja, intresserad","Inte sÃ¤ker â€” berÃ¤tta mer","Nej, behÃ¶vs inte"],phase:"preferences",prog:97},
  {msg:"Vilket sprÃ¥k ska din bankir tala?",field:"bankerLanguage",type:"select",opts:["Finska","Svenska","Engelska","Ingen preferens"],phase:"preferences",prog:98},
  {msg:"PÃ¥ vilket sprÃ¥k vill du ha dina rapporter?",field:"reportLanguage",type:"select",opts:["Finska","Svenska","Engelska"],phase:"preferences",prog:99},
  {msg:"Sista frÃ¥gan. Vilken e-post ska vi anvÃ¤nda?",field:"email",type:"text",ph:"din@email.se",phase:"preferences",prog:100},
]};


const KYC_COMPLETE={
  en:{
    full:{msg:"Thank you! Your profile is complete. Noah will review it personally and begin sourcing proposals from our 29 banks within 48 hours. You'll receive an email confirmation shortly.",cta:"We'll be in touch"},
    partial:{msg:"Perfect! Noah will send you a warm email shortly with the information you've shared. He'll ask a few follow-up questions to understand your investment approach, then begin sourcing the perfect banking proposals for you. Expect his email within 24 hours.",cta:"Check your email"}
  },
  fi:{
    full:{msg:"Kiitos! Profiilisi on valmis. Noah kÃ¤y sen henkilÃ¶kohtaisesti lÃ¤pi ja aloittaa tarjousten hankinnan 29 pankiltamme 48 tunnin kuluessa. Saat sÃ¤hkÃ¶postivahvistuksen pian.",cta:"Olemme yhteydessÃ¤"},
    partial:{msg:"TÃ¤ydellinen! Noah lÃ¤hettÃ¤Ã¤ sinulle lÃ¤mpimÃ¤n sÃ¤hkÃ¶postin pian jakamillasi tiedoilla. HÃ¤n kysyy muutaman jatkokysymyksen ymmÃ¤rtÃ¤Ã¤kseen sijoituslÃ¤hestymistapasi, ja alkaa sitten hankkia tÃ¤ydellisiÃ¤ pankkitarjouksia sinulle. Odota hÃ¤nen sÃ¤hkÃ¶postiaan 24 tunnin sisÃ¤llÃ¤.",cta:"Tarkista sÃ¤hkÃ¶postisi"}
  },
  sv:{
    full:{msg:"Tack! Din profil Ã¤r klar. Noah kommer att granska den personligen och bÃ¶rja skaffa fÃ¶rslag frÃ¥n vÃ¥ra 29 banker inom 48 timmar. Du fÃ¥r en bekrÃ¤ftelse via e-post snart.",cta:"Vi hÃ¶r av oss"},
    partial:{msg:"Perfekt! Noah kommer att skicka dig ett varmt e-postmeddelande inom kort med den information du har delat. Han kommer att stÃ¤lla nÃ¥gra uppfÃ¶ljningsfrÃ¥gor fÃ¶r att fÃ¶rstÃ¥ din investeringsansats och sedan bÃ¶rja skaffa de perfekta bankfÃ¶rslagen fÃ¶r dig. FÃ¶rvÃ¤nta dig hans e-post inom 24 timmar.",cta:"Kolla din e-post"}
  }
};

function KYC({open,onClose,lang,t}){
  const[step,setStep]=useState(0);
  const[prof,setProf]=useState({});
  const[inp,setInp]=useState("");
  const[multi,setMulti]=useState([]);
  const[done,setDone]=useState(false);
  const[partial,setPartial]=useState(false); // Track if user chose email Noah
  const[msgs,setMsgs]=useState([]);
  const[anim,setAnim]=useState(false);
  const eR=useRef(null);
  const steps=KYC_STEPS[lang]||KYC_STEPS.en;
  const cur=steps[step];
  const prog=done?100:(cur?.prog||0);
  const phase=done?"summary":(cur?.phase||"welcome");

  useEffect(()=>{setTimeout(()=>eR.current?.scrollIntoView({behavior:"smooth"}),100)},[msgs,step]);
  useEffect(()=>{
    if(open&&msgs.length===0){
      setAnim(true);
      setTimeout(()=>{setMsgs([{role:"assistant",content:steps[0].msg}]);setAnim(false)},600);
    }
  },[open]);

  const advance=(val,emailNoah=false)=>{
    // Record answer
    if(cur?.field&&val){
      setProf(p=>({...p,[cur.field]:val}));
    }
    // Add user message
    if(val){
      const display=Array.isArray(val)?val.join(", "):val;
      setMsgs(p=>[...p,{role:"user",content:display}]);
    }
    
    // Handle "Email Noah" option
    if(emailNoah){
      setPartial(true);
      setDone(true);
      setAnim(true);
      setTimeout(()=>{
        const comp=(KYC_COMPLETE[lang]||KYC_COMPLETE.en).partial;
        setMsgs(p=>[...p,{role:"assistant",content:comp.msg}]);
        setAnim(false);
      },600);
      return;
    }
    
    // Next step
    const next=step+1;
    if(next<steps.length){
      setStep(next);
      setInp("");setMulti([]);
      setAnim(true);
      setTimeout(()=>{
        setMsgs(p=>[...p,{role:"assistant",content:steps[next].msg}]);
        setAnim(false);
      },500);
    }else{
      // Complete - full profile
      setDone(true);
      setAnim(true);
      setTimeout(()=>{
        const comp=(KYC_COMPLETE[lang]||KYC_COMPLETE.en).full;
        setMsgs(p=>[...p,{role:"assistant",content:comp.msg}]);
        setAnim(false);
      },600);
    }
  };

  const toggleMulti=(v)=>setMulti(p=>p.includes(v)?p.filter(x=>x!==v):[...p,v]);
  const submitText=()=>{const v=inp.trim();if(!v)return;advance(v)};
  const submitMulti=()=>{if(multi.length===0)return;advance(multi)};

  const allF=t.pf.flatMap(s=>s[1]);
  const filled=allF.filter(f=>{const v=prof[f[0]];return v&&String(v).trim()!==""}).length;
  const[brief,setBrief]=useState(false);

  const phaseLabel=(()=>{
    const idx=["welcome","personal","professional","financial","needs","jurisdictions","preferences","summary"].indexOf(phase);
    return t.phases[Math.min(idx,t.phases.length-1)]||phase;
  })();

  return(
    <>
    {open&&<div className="ky-overlay" onClick={onClose}/>}
    <div className={"ky"+(open?" open":"")}>
      <div className="ky-h">
        <div className="ky-hl"><div className="ky-dia"/><div><div className="ky-ht">{lang==="fi"?"Turvallinen liittyminen":lang==="sv"?"SÃ¤ker introduktion":"Secure Onboarding"}</div><div className="ky-hp">{phaseLabel}</div></div></div>
        <div className="ky-hr"><button className={"ky-bb"+(brief?" on":"")} onClick={()=>setBrief(v=>!v)}>Profile{filled>0?(" Â· "+filled):""}</button><button className="ky-x" onClick={onClose}>{"\u2715"}</button></div>
      </div>
      <div className="ky-prog"><div className="ky-prog-f" style={{width:prog+"%"}}/></div>
      <div className="ky-body">{brief?
        <div className="ky-bf">{t.pf.map(s=><div key={s[0]} className="ky-bs"><div className="ky-bst">{s[0]}</div>{s[1].map(f=>{const v=prof[f[0]];const d=v?(Array.isArray(v)?v.join(", "):String(v)):null;return<div key={f[0]} className="ky-br"><span className="ky-bk">{f[1]}</span>{d?<span className="ky-bv">{d}</span>:<span className="ky-be">-</span>}</div>})}</div>)}</div>:
        <div className="ky-chat">
          {msgs.map((m,i)=><div key={i} className="ky-m">{m.role==="assistant"?
            <div className="ky-ma"><div className="ky-av"/><div><div className="ky-ba">{m.content}</div></div></div>:
            <div className="ky-mu"><div className="ky-bu">{m.content}</div></div>}</div>)}
          {anim&&<div className="ky-m"><div className="ky-ma"><div className="ky-av"/><div className="ky-ty"><span/><span/><span/></div></div></div>}
          <div ref={eR}/>
        </div>}
      </div>

      {/* Input area */}
      {!brief&&!done&&!anim&&cur&&(()=>{
        // Welcome step â€” just a button
        if(step===0&&cur.qr){
          return <div className="ky-ia"><div className="ky-qr-wrap">{cur.qr.map((q,i)=><button key={i} className="ky-qrb" onClick={()=>advance(null)}>{q}</button>)}</div><div className="ky-sn"><Lock s={10}/>{t.kyc[2]}</div></div>;
        }
        // Text input
        if(cur.type==="text"){
          return <div className="ky-ia"><div className="ky-ir"><input className="ky-ii" type={cur.field==="email"?"email":"text"} placeholder={cur.ph||""} value={inp} onChange={e=>setInp(e.target.value)} onKeyDown={e=>{if(e.key==="Enter")submitText()}} autoFocus/>
            <button className="ky-se" onClick={submitText} disabled={!inp.trim()}>{"\u2192"}</button></div>
            <div className="ky-sn"><Lock s={10}/>{t.kyc[2]}</div></div>;
        }
        // Single select
        if(cur.type==="select"){
          return <div className="ky-ia"><div className="ky-qr-wrap">{cur.opts.map((o,i)=><button key={i} className="ky-qrb" onClick={()=>advance(o)}>{o}</button>)}</div><div className="ky-sn"><Lock s={10}/>{t.kyc[2]}</div></div>;
        }
        // Multi select
        if(cur.type==="multi"){
          return <div className="ky-ia"><div className="ky-qr-wrap">{cur.opts.map((o,i)=><button key={i} className={"ky-qrb"+(multi.includes(o)?" on":"")} onClick={()=>toggleMulti(o)}>{multi.includes(o)?"\u2713 ":""}{o}</button>)}</div>
            {multi.length>0&&<button className="ky-confirm" onClick={submitMulti}>{lang==="fi"?"Jatka":lang==="sv"?"FortsÃ¤tt":"Continue"} ({multi.length})</button>}
            <div className="ky-sn"><Lock s={10}/>{t.kyc[2]}</div></div>;
        }
        // Checkpoint - choice between continue or email Noah
        if(cur.type==="checkpoint"||cur.type==="checkpoint2"){
          return <div className="ky-ia"><div className="ky-qr-wrap">{cur.opts.map((o,i)=>{
            const isEmailNoah=i===1; // Second option is always "Email Noah"
            return <button key={i} className="ky-qrb" onClick={()=>advance(o,isEmailNoah)}>{o}</button>;
          })}</div><div className="ky-sn"><Lock s={10}/>{t.kyc[2]}</div></div>;
        }
        return null;
      })()}

      {/* Done state */}
      {!brief&&done&&!anim&&<div className="ky-ia"><div className="ky-done">
        <button className="btn-p" onClick={onClose}><span>{partial?(KYC_COMPLETE[lang]||KYC_COMPLETE.en).partial.cta:(KYC_COMPLETE[lang]||KYC_COMPLETE.en).full.cta}</span></button>
      </div><div className="ky-sn"><Lock s={10}/>{t.kyc[2]}</div></div>}
    </div>
    </>
  );
}

/* â•â•â• WEALTH ESTIMATOR â€” v15: band-based AUM + auto fee calculation â•â•â• */
const AUM_BANDS=[
  {l:"\u20AC250K",v:250000,s:"\u20AC250,000"},
  {l:"\u20AC500K",v:500000,s:"\u20AC500,000"},
  {l:"\u20AC1M",v:1000000,s:"\u20AC1,000,000"},
  {l:"\u20AC2M",v:2000000,s:"\u20AC2,000,000"},
  {l:"\u20AC5M",v:5000000,s:"\u20AC5,000,000"},
  {l:"\u20AC10M",v:10000000,s:"\u20AC10,000,000"},
  {l:"\u20AC20M",v:20000000,s:"\u20AC20,000,000"},
  {l:"\u20AC40M",v:40000000,s:"\u20AC40,000,000"},
  {l:"\u20AC60M",v:60000000,s:"\u20AC60,000,000"},
  {l:"\u20AC100M",v:100000000,s:"\u20AC100,000,000"},
];
const getFees=(amt)=>{
  // Typical all-in fees decrease with AUM (industry standard)
  let typFee;
  if(amt<=1000000) typFee=1.80;
  else if(amt<=5000000) typFee=1.50;
  else if(amt<=10000000) typFee=1.25;
  else if(amt<=30000000) typFee=1.05;
  else if(amt<=60000000) typFee=0.90;
  else typFee=0.75;
  // v27/v28: Fee layer breakdown (proportional to total) â€” FX is the single largest hidden cost
  const layers=[
    {k:"mgmt",  p:0.30},  // Management fee â€” the "headline" number
    {k:"fx",    p:0.22},  // FX spreads â€” largest hidden cost
    {k:"fund",  p:0.20},  // Underlying fund costs (hidden)
    {k:"txn",   p:0.12},  // Transaction costs
    {k:"cust",  p:0.09},  // Custody fee
    {k:"plat",  p:0.07},  // Platform & account charges
  ];
  const feeBreak=layers.map(l=>({k:l.k,v:+(typFee*l.p).toFixed(2)}));
  // Adjust rounding so layers sum to typFee exactly
  const layerSum=feeBreak.reduce((s,l)=>s+l.v,0);
  if(Math.abs(layerSum-typFee)>0.005) feeBreak[0].v=+(feeBreak[0].v+(typFee-layerSum)).toFixed(2);
  // Aureum fee tiers
  let aurPct;
  if(amt<2000000) aurPct=0.15;
  else if(amt<=15000000) aurPct=0.10;
  else aurPct=0.05;
  // Minimum fee â‚¬500/yr
  const aurAbs=Math.max(500,amt*aurPct/100);
  const aurEffective=aurAbs/(amt/100);
  // Aureum saving = typical all-in vs Aureum-negotiated all-in
  let saving;
  if(amt<=10000000) saving=0.50;
  else if(amt<=30000000) saving=0.30;
  else saving=0.20;
  return {typFee, aurFee: typFee-saving, saving, aurPct, aurEffective, feeBreak};
};

function WealthEst({t,lang}){
  const[bandIdx,setBandIdx]=useState(3); // Default â‚¬2M
  const[yrs,setYrs]=useState(15);
  const[gross,setGross]=useState(6.0);
  const amt=AUM_BANDS[bandIdx].v;
  const{typFee,aurFee,saving,aurPct,aurEffective,feeBreak}=getFees(amt);
  const fmt=v=>v>=1e6?("\u20AC"+(v/1e6).toFixed(v>=10e6?0:v>=1e6?1:2)+"M"):v>=1e3?("\u20AC"+Math.round(v/1e3).toLocaleString()+"K"):("\u20AC"+v);
  const fmtF=v=>"\u20AC"+Math.round(v).toLocaleString();
  const data=[];
  for(let y=0;y<=yrs;y++){data.push({y:y,typ:Math.round(amt*Math.pow(1+(gross-typFee)/100,y)/1000),aur:Math.round(amt*Math.pow(1+(gross-aurFee)/100,y)/1000)})}
  // Clean Y-axis: compute even ticks
  const dMin=data[0].typ;
  const dMax=data[data.length-1].aur;
  const range=dMax-dMin;
  // Find step that gives 3-5 ticks across the range
  const mag=Math.pow(10,Math.floor(Math.log10(Math.max(range,1))));
  const candidates=[mag*0.1,mag*0.2,mag*0.25,mag*0.5,mag,mag*2,mag*2.5,mag*5];
  const step=candidates.find(s=>s>0&&Math.ceil(range/s)>=2&&Math.ceil(range/s)<=5)||(mag||1);
  const tickStart=Math.floor(dMin/step)*step;
  const tickEnd=Math.ceil(dMax/step)*step;
  const yTicks=[];for(let v=tickStart;v<=tickEnd;v+=step)yTicks.push(Math.round(v));
  const yDom=[tickStart,tickEnd];
  const fT=amt*Math.pow(1+(gross-typFee)/100,yrs);
  const fA=amt*Math.pow(1+(gross-aurFee)/100,yrs);
  const diff=fA-fT;
  const aurAnnual=Math.max(500,amt*aurPct/100);
  const aurTotal=aurAnnual*yrs;
  const roi=diff/aurTotal;
  const presets=[
    {l:t.we[3][0],g:4},
    {l:t.we[3][1],g:6},
    {l:t.we[3][2],g:8}];

  return(
    <div className="calc">
      <div className="we-presets">
        {presets.map((p,i)=><button key={i} className={"we-pre"+(gross===p.g?" on":"")} onClick={()=>setGross(p.g)}>{p.l}</button>)}
      </div>
      <div className="we-grid">
        {/* AUM Band Selector */}
        <div className="we-sl">
          <div className="we-sl-top"><span className="we-sl-l">{t.we[0]}</span><span className="we-sl-v">{AUM_BANDS[bandIdx].l}</span></div>
          <div className="we-bands">
            {AUM_BANDS.map((b,i)=><button key={i} className={"we-band"+(bandIdx===i?" on":"")} onClick={()=>setBandIdx(i)}>{b.l}</button>)}
          </div>
        </div>
        {/* Time horizon */}
        <div className="we-sl">
          <div className="we-sl-top"><span className="we-sl-l">{t.we[1]}</span><span className="we-sl-v">{yrs} {t.we[5]}</span></div>
          <input type="range" className="calc-rng" min={5} max={30} step={1} value={yrs} onChange={e=>setYrs(+e.target.value)}/>
          <div className="we-sl-mm"><span>5</span><span>30</span></div>
        </div>
        {/* Fee comparison â€” v27: layered breakdown */}
        <div className="we-fee-compare">
          <div className="we-fee-box typ">
            <div className="we-fee-label">{lang==="fi"?"Tyypillinen kokonaiskulu":lang==="sv"?"Typisk totalkostnad":"Typical total cost"}</div>
            <div className="we-fee-val">{typFee.toFixed(2)}%</div>
            <div className="we-fee-abs">{fmtF(Math.round(amt*typFee/100))}/{lang==="fi"?"v":lang==="sv"?"Ã¥r":"yr"}</div>
            <div className="we-layers">
              {feeBreak.map(l=><div key={l.k} className="we-layer">
                <span className="we-layer-bar" style={{width:Math.max(8,l.v/typFee*100)+"%"}}/>
                <span className="we-layer-name">{({mgmt:{en:"Management fee",fi:"Hallinnointipalkkio",sv:"FÃ¶rvaltningsavgift"},fx:{en:"FX spreads (hidden)",fi:"Valuuttamarginaalit (piilossa)",sv:"Valutamarginaler (dolda)"},fund:{en:"Fund costs (hidden)",fi:"Rahastokulut (piilossa)",sv:"Fondkostnader (dolda)"},txn:{en:"Transaction costs",fi:"Transaktiokulut",sv:"Transaktionskostnader"},cust:{en:"Custody fee",fi:"SÃ¤ilytyspalkkio",sv:"DepÃ¥fÃ¶rvaringsavgift"},plat:{en:"Platform & account",fi:"Alusta & tilit",sv:"Plattform & konto"}})[l.k][lang]}</span>
                <span className="we-layer-val">{l.v.toFixed(2)}%</span>
              </div>)}
            </div>
          </div>
          <div className="we-fee-arrow">{"\u2192"}</div>
          <div className="we-fee-box aur">
            <div className="we-fee-label">{lang==="fi"?"Aureumin kautta (kokonaiskulu)":lang==="sv"?"Med Aureum (totalkostnad)":"With Aureum (all-in)"}</div>
            <div className="we-fee-val">{aurFee.toFixed(2)}%</div>
            <div className="we-fee-abs">{fmtF(Math.round(amt*aurFee/100))}/{lang==="fi"?"v":lang==="sv"?"Ã¥r":"yr"}</div>
            <div className="we-aur-note">{lang==="fi"?"Sis. institutionaaliset osuusluokat":lang==="sv"?"Inkl. institutionella andelsklasser":"Incl. institutional share classes"}</div>
          </div>
          <div className="we-fee-save">
            <div className="we-fee-save-val">{"\u2212"}{saving.toFixed(2)}%</div>
            <div className="we-fee-save-lbl">{lang==="fi"?"sÃ¤Ã¤stÃ¶":lang==="sv"?"besparing":"saving"}</div>
          </div>
        </div>
      </div>
      <div className="we-chart">
        <div className="we-legend"><span className="we-leg"><span className="rp-dot" style={{background:"#C9A96E"}}/>With Aureum (net {(gross-aurFee).toFixed(1)}%)</span><span className="we-leg"><span className="rp-dot" style={{background:"#637896"}}/>Typical (net {(gross-typFee).toFixed(1)}%)</span></div>
        <ResponsiveContainer width="100%" height={230}>
          <AreaChart data={data} margin={{top:10,right:10,bottom:0,left:-10}}>
            <defs><linearGradient id="gAu" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stopColor="#C9A96E" stopOpacity={0.3}/><stop offset="100%" stopColor="#C9A96E" stopOpacity={0.02}/></linearGradient></defs>
            <CartesianGrid strokeDasharray="3 3" stroke="#1A3258" vertical={false}/>
            <XAxis dataKey="y" tick={{fontSize:10,fill:"#637896"}} axisLine={false} tickLine={false} interval={Math.max(1,Math.floor(yrs/5))} tickFormatter={v=>"Yr "+v}/>
            <YAxis tick={{fontSize:10,fill:"#637896"}} axisLine={false} tickLine={false} tickFormatter={v=>v>=1000?(v/1000).toFixed(0)+"M":v+"K"} domain={yDom} ticks={yTicks}/>
            <Tooltip contentStyle={{background:"#0E2344",border:"1px solid #1A3258",borderRadius:6,fontSize:11}} formatter={v=>v>=1000?"\u20AC"+(v/1000).toFixed(1)+"M":"\u20AC"+v+"K"} labelFormatter={v=>"Year "+v}/>
            <Area type="monotone" dataKey="aur" name="Aureum" stroke="#C9A96E" strokeWidth={3} fill="url(#gAu)"/>
            <Area type="monotone" dataKey="typ" name="Typical" stroke="#637896" strokeWidth={1.5} fill="none" strokeDasharray="5 3"/>
          </AreaChart>
        </ResponsiveContainer>
      </div>
      <div className="we-results">
        <div className="we-r"><div className="we-rl">{lang==="fi"?"Tyypillinen":lang==="sv"?"Typisk":"Typical"} {yrs}{lang==="fi"?"v":lang==="sv"?"Ã¥r":"y"}</div><div className="we-rv">{fmtF(fT)}</div></div>
        <div className="we-r hi"><div className="we-rl">{lang==="fi"?"Aureumilla":lang==="sv"?"Med Aureum":"With Aureum"}</div><div className="we-rv gold">{fmtF(fA)}</div></div>
        <div className="we-r"><div className="we-rl">{lang==="fi"?"PidÃ¤t enemmÃ¤n":lang==="sv"?"Du behÃ¥ller mer":"You keep more"}</div><div className="we-rv green">+{fmtF(diff)}</div><div className="we-rs">{roi.toFixed(0)}x {lang==="fi"?"Aureum-maksu":lang==="sv"?"Aureum-avgift":"Aureum fee"}</div></div>
      </div>
      {/* v28: How We Are Compensated â€” removed in v29, details in FAQ */}
      <div className="calc-fn">* {lang==="fi"?"Ainoastaan havainnollistavaa. Aiempi tuotto ei ennusta tulevaa.":lang==="sv"?"Enbart illustrativt. Tidigare avkastning fÃ¶rutsÃ¤ger inte framtida.":"Illustrative only. Past returns do not predict future performance."} {lang==="fi"?"Aureum ei tarjoa sijoitusneuvontaa.":lang==="sv"?"Aureum ger inte investeringsrÃ¥d.":"Aureum does not provide investment advice."}</div>
    </div>
  );
}

/* â•â•â• MONTHLY REPORT â€” v17: full FT-style with holdings, winners, losers â•â•â• */
function RPV({lang}){
  const alloc_total = ALLOC.reduce((s,a)=>s+a.v,0);
  const allocNames=getAllocNames(lang);
  const ccyOther=getCcyOther(lang);
  const t = lang==="fi" ? {
    tag:"Kuukausiraportti", date:"Joulukuu 2025", portVal:"Salkun arvo", dec:"Joulukuu", ytd:"Vuoden alusta",
    peerRank:"Vertailussa", allInCost:"Kokonaiskulut", perf12:"Tuotto Â· 12 kuukautta",
    portfolio:"Salkku", benchmark:"Pankin vertailuindeksi", realBench:"Oikea vertailuindeksi",
    assetAlloc:"Varallisuusjakauma", ccyExp:"Valuuttajakauma", largeHold:"Suurimmat omistukset",
    holding:"Omistus", sector:"Sektori", weight:"Paino", value:"Arvo", month:"Kuukausi",
    topPerf:"â–² Parhaat tuotot vuoden alusta", underPerf:"â–¼ Heikoimmat tuotot vuoden alusta",
    costSum:"Kuluyhteenveto", allIn:"YhteensÃ¤", bank:"Pankki", custody:"SÃ¤ilytys",
    transactions:"Transaktiot", funds:"Rahastot", fxSpreads:"Valuuttamarginaalit", aureumFee:"Aureum"
  } : lang==="sv" ? {
    tag:"MÃ¥nadsrapport", date:"December 2025", portVal:"PortfÃ¶ljvÃ¤rde", dec:"December", ytd:"Hittills i Ã¥r",
    peerRank:"JÃ¤mfÃ¶relse", allInCost:"Totalkostnad", perf12:"Avkastning Â· 12 mÃ¥nader",
    portfolio:"PortfÃ¶lj", benchmark:"Bankens jÃ¤mfÃ¶relseindex", realBench:"Korrekt jÃ¤mfÃ¶relseindex",
    assetAlloc:"TillgÃ¥ngsfÃ¶rdelning", ccyExp:"Valutaexponering", largeHold:"StÃ¶rsta innehav",
    holding:"Innehav", sector:"Sektor", weight:"Vikt", value:"VÃ¤rde", month:"MÃ¥nad",
    topPerf:"â–² BÃ¤sta avkastning hittills i Ã¥r", underPerf:"â–¼ SÃ¤msta avkastning hittills i Ã¥r",
    costSum:"Kostnadssammanfattning", allIn:"Totalt", bank:"Bank", custody:"FÃ¶rvaring",
    transactions:"Transaktioner", funds:"Fonder", fxSpreads:"Valutamarginaler", aureumFee:"Aureum"
  } : {
    tag:"Monthly Report", date:"December 2025", portVal:"Portfolio Value", dec:"December", ytd:"YTD",
    peerRank:"Peer Rank", allInCost:"All-in Cost", perf12:"Performance Â· 12 Months",
    portfolio:"Portfolio", benchmark:"Bank's Benchmark", realBench:"Proper Benchmark",
    assetAlloc:"Asset Allocation", ccyExp:"Currency Exposure", largeHold:"Largest Holdings",
    holding:"Holding", sector:"Sector", weight:"Weight", value:"Value", month:"Month",
    topPerf:"â–² Top Performers YTD", underPerf:"â–¼ Underperformers YTD",
    costSum:"Cost Summary", allIn:"All-in", bank:"Bank", custody:"Custody",
    transactions:"Transactions", funds:"Funds", fxSpreads:"FX Spreads", aureumFee:"Aureum"
  };
  return(
    <div className="mr">
      {/* Masthead */}
      <div className="mr-mast">
        <div className="mr-mast-left"><span className="mr-mast-tag">{t.tag}</span><span className="mr-mast-date">{t.date}</span></div>
        <div className="mr-mast-right"><span className="mr-mast-acct">Lombard Odier Â· Geneva</span><span className="mr-mast-id">AU-2025-0847</span></div>
      </div>
      {/* Hero KPIs */}
      <div className="mr-hero">
        <div className="mr-hero-main"><div className="mr-hero-label">{t.portVal}</div><div className="mr-hero-val">{"\u20AC2,164,000"}</div></div>
        <div className="mr-hero-kpis">
          <div className="mr-kpi"><div className="mr-kv green">+1.8%</div><div className="mr-kl">{t.dec}</div></div>
          <div className="mr-kpi"><div className="mr-kv green">+8.2%</div><div className="mr-kl">{t.ytd}</div></div>
          <div className="mr-kpi"><div className="mr-kv gold">Top 40%</div><div className="mr-kl">{t.peerRank}</div></div>
          <div className="mr-kpi"><div className="mr-kv">1.25%</div><div className="mr-kl">{t.allInCost}</div></div>
        </div>
      </div>
      {/* Performance chart */}
      <div className="mr-section">
        <div className="mr-sh">{t.perf12}</div>
        <div className="mr-chart-leg"><span className="mr-leg"><span className="rp-dot" style={{background:"#0D4F8B"}}/>{t.portfolio} +8.2%</span><span className="mr-leg"><span className="rp-dot" style={{background:"#C9975C"}}/>{t.benchmark} +6.0%</span><span className="mr-leg"><span className="rp-dot" style={{background:"#27AE60"}}/>{t.realBench} +18.0%</span></div>
        <ResponsiveContainer width="100%" height={140}>
          <AreaChart data={PORT_H} margin={{top:4,right:4,bottom:0,left:-20}}>
            <defs><linearGradient id="gMr" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stopColor="#0D4F8B" stopOpacity={0.1}/><stop offset="100%" stopColor="#0D4F8B" stopOpacity={0}/></linearGradient></defs>
            <CartesianGrid strokeDasharray="3 3" stroke="#E5DDD0" vertical={false}/>
            <XAxis dataKey="m" tick={{fontSize:9,fill:"#999"}} axisLine={false} tickLine={false}/>
            <YAxis tick={{fontSize:9,fill:"#999"}} axisLine={false} tickLine={false} tickFormatter={v=>v+"K"} domain={['dataMin-5','dataMax+5']}/>
            <Area type="monotone" dataKey="v" stroke="#0D4F8B" strokeWidth={2} fill="url(#gMr)"/>
            <Area type="monotone" dataKey="b" stroke="#C9975C" strokeWidth={1.2} fill="none" strokeDasharray="4 3"/>
            <Area type="monotone" dataKey="rb" stroke="#27AE60" strokeWidth={1.5} fill="none" strokeDasharray="2 2"/>
          </AreaChart>
        </ResponsiveContainer>
      </div>
      {/* Allocation + Currency side by side */}
      <div className="mr-two-col">
        <div className="mr-col">
          <div className="mr-sh">{t.assetAlloc}</div>
          <div className="rp-stack-bar" style={{height:12,marginBottom:6}}>{ALLOC.map((a,i)=><div key={i} className="rp-stack-seg" style={{width:(a.v/alloc_total*100)+"%",background:a.c}} title={allocNames[i]}/>)}</div>
          <div className="mr-alloc-list">{ALLOC.map((a,i)=><div key={i} className="mr-alloc-item"><span className="rp-dot" style={{background:a.c}}/><span className="mr-alloc-name">{allocNames[i]}</span><span className="mr-alloc-pct">{a.v}%</span></div>)}</div>
        </div>
        <div className="mr-col">
          <div className="mr-sh">{t.ccyExp}</div>
          <div className="mr-ccy-list">{CCY.map((c,i)=><div key={i} className="mr-ccy-item"><div className="mr-ccy-bar-wrap"><div className="mr-ccy-bar" style={{width:c.w,background:c.clr}}/></div><span className="mr-ccy-code">{c.c==="Other"?ccyOther:c.c}</span><span className="mr-ccy-pct">{c.w}</span></div>)}</div>
        </div>
      </div>
      {/* Largest Holdings table */}
      <div className="mr-section">
        <div className="mr-sh">{t.largeHold}</div>
        <div className="mr-tbl">
          <div className="mr-tbl-hdr"><span className="mr-th" style={{flex:2}}>{t.holding}</span><span className="mr-th">{t.sector}</span><span className="mr-th r">{t.weight}</span><span className="mr-th r">{t.value}</span><span className="mr-th r">{t.ytd}</span><span className="mr-th r">{t.month}</span></div>
          {HOLDINGS.map((h,i)=><div key={i} className={"mr-tbl-row"+(i%2===0?" alt":"")}>
            <span className="mr-td" style={{flex:2,fontWeight:500}}>{h.n}</span>
            <span className="mr-td mr-td-sec">{translateSector(h.sec,lang)}</span>
            <span className="mr-td r">{h.w}</span>
            <span className="mr-td r">{h.val}</span>
            <span className={"mr-td r "+(h.ytd.startsWith("-")?"red":"grn")}>{h.ytd}</span>
            <span className={"mr-td r "+(h.chg.startsWith("-")?"red":h.chg==="0.0%"?"":"grn")}>{h.chg}</span>
          </div>)}
        </div>
      </div>
      {/* Winners & Losers */}
      <div className="mr-two-col">
        <div className="mr-col">
          <div className="mr-sh mr-sh-icon">{t.topPerf}</div>
          {WINNERS.map((w,i)=><div key={i} className="mr-wl-row"><span className="mr-wl-n">{w.n}</span><span className="mr-wl-r grn">{w.r}</span><span className="mr-wl-c">{w.c}</span></div>)}
        </div>
        <div className="mr-col">
          <div className="mr-sh mr-sh-icon">{t.underPerf}</div>
          {LOSERS.map((w,i)=><div key={i} className="mr-wl-row"><span className="mr-wl-n">{w.n}</span><span className="mr-wl-r red">{w.r}</span><span className="mr-wl-c">{w.c}</span></div>)}
        </div>
      </div>
      {/* Fee summary â€” compact */}
      <div className="mr-section mr-fees">
        <div className="mr-sh">{t.costSum}</div>
        <div className="mr-fee-line-compact">
          <span>{t.allIn}: <strong>1.25%</strong></span>
          <span className="mr-fee-sep">{"\u00B7"}</span>
          <span>{t.bank} 0.70%</span>
          <span className="mr-fee-sep">{"\u00B7"}</span>
          <span>{t.custody} 0.10%</span>
          <span className="mr-fee-sep">{"\u00B7"}</span>
          <span>{t.transactions} 0.15%</span>
          <span className="mr-fee-sep">{"\u00B7"}</span>
          <span>Funds 0.20%</span>
          <span className="mr-fee-sep">{"\u00B7"}</span>
          <span className="mr-fee-au">Aureum 0.10%</span>
        </div>
        <div className="mr-fee-selling">{"\u2713"} No hidden fees {"\u00B7"} No commissions {"\u00B7"} No kickbacks</div>
      </div>
      <div className="mr-disc">This material is for informational purposes only and does not constitute investment advice. Past performance does not predict future results. Prepared by Aureum Private Office under power of attorney.</div>
    </div>
  );
}

/* â•â•â• WHATSAPP â•â•â• */
function WAP(){
  return(
    <div className="wa"><div className="wa-h"><div className="wa-ava">A</div><div><div className="wa-name">Aureum Insights</div><div className="wa-st">Online</div></div></div>
      <div className="wa-body">{WA.map((m,i)=>
        <div key={i} className={"wa-m "+m.f}><div className={"wa-b "+m.f}>{m.t.split("\n").map((l,li)=><span key={li}>{l}{li<m.t.split("\n").length-1&&<br/>}</span>)}<div className="wa-tm">{m.tm}</div></div></div>
      )}</div>
    </div>
  );
}

/* â•â•â• CLIENT PORTAL â•â•â• */
function Portal({lang,t}){
  const[tab,setTab]=useState("overview");
  const tabs=[
    ["overview",lang==="fi"?"Yleiskatsaus":lang==="sv"?"Ã–versikt":"Overview"],
    ["proposals",lang==="fi"?"Tarjoukset":lang==="sv"?"FÃ¶rslag":"Proposals"],
    ["reports",lang==="fi"?"Raportit":lang==="sv"?"Rapporter":"Reports"],
    ["meetings",lang==="fi"?"Tapaamiset":lang==="sv"?"MÃ¶ten":"Meetings"]
  ];
  return(
    <div className="portal">
      <div className="portal-hd"><div className="portal-user"><div className="portal-av">JV</div><div><div className="portal-nm">Jari Virtanen</div><div className="portal-id">AU-2025-0847 Â· {lang==="fi"?"Aktiivinen":lang==="sv"?"Aktiv":"Active"}</div></div></div>
        <div className="portal-meta"><div><span className="portal-ml">{lang==="fi"?"Salkunhoitaja":lang==="sv"?"FÃ¶rvaltare":"Manager"}</span><span className="portal-mv">Lombard Odier</span></div><div><span className="portal-ml">{lang==="fi"?"Kieli":lang==="sv"?"SprÃ¥k":"Language"}</span><span className="portal-mv">{"\u{1F1EB}\u{1F1EE}"} Suomi</span></div></div></div>
      <div className="portal-tabs">{tabs.map(([k,l])=><button key={k} className={"portal-tab"+(tab===k?" on":"")} onClick={()=>setTab(k)}>{l}</button>)}</div>
      <div className="portal-body">
        {tab==="overview"&&<div>
          <div className="portal-kpis">{[
            {v:"\u20AC2,164,000",l:lang==="fi"?"Salkun arvo":lang==="sv"?"PortfÃ¶ljvÃ¤rde":"Portfolio Value",c:""},
            {v:"+8.2%",l:lang==="fi"?"Vuosituotto":lang==="sv"?"Ã…rsavkastning":"YTD Return",c:"green"},
            {v:"Top 40%",l:lang==="fi"?"Vertailussa":lang==="sv"?"JÃ¤mfÃ¶relse":"Peer Ranking",c:"gold"},
            {v:"1.25%",l:lang==="fi"?"Kokonaiskulut":lang==="sv"?"Totalkostnad":"All-in Cost",c:""}
          ].map((k,i)=>
            <div key={i} className="portal-kpi"><div className={"portal-kv "+(k.c||"")}>{k.v}</div><div className="portal-kl">{k.l}</div></div>)}</div>
          <div className="portal-chart"><ResponsiveContainer width="100%" height={160}>
            <AreaChart data={PORT_H} margin={{top:5,right:5,bottom:0,left:-10}}>
              <defs><linearGradient id="gPt" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stopColor="#4A8FD4" stopOpacity={0.15}/><stop offset="100%" stopColor="#4A8FD4" stopOpacity={0}/></linearGradient></defs>
              <CartesianGrid strokeDasharray="3 3" stroke="#F0EDE8" vertical={false}/>
              <XAxis dataKey="m" tick={{fontSize:9,fill:"#999"}} axisLine={false} tickLine={false}/>
              <YAxis tick={{fontSize:9,fill:"#999"}} axisLine={false} tickLine={false} tickFormatter={v=>"\u20AC"+v+"K"} domain={['dataMin-5','dataMax+5']}/>
              <Area type="monotone" dataKey="v" stroke="#4A8FD4" strokeWidth={2} fill="url(#gPt)"/>
              <Area type="monotone" dataKey="b" stroke="#C9A96E" strokeWidth={1} fill="none" strokeDasharray="4 3"/>
            </AreaChart>
          </ResponsiveContainer></div>
          <div className="portal-act-t">{lang==="fi"?"ViimeisimmÃ¤t":lang==="sv"?"Senaste aktivitet":"Recent Activity"}</div>
          {[
            {d:"15 Dec",t:lang==="fi"?"Kuukausiraportti valmis":lang==="sv"?"MÃ¥nadsrapport klar":"Monthly report ready",s:"report"},
            {d:"12 Dec",t:"WhatsApp: Novo Nordisk +4.2%",s:"insight"},
            {d:"1 Dec",t:lang==="fi"?"NeljÃ¤nnesmaksu EUR 578":lang==="sv"?"Q4-avgift EUR 578 debiterad":"Q4 fee EUR 578 debited",s:"fee"},
            {d:"28 Nov",t:lang==="fi"?"Vertailuanalyysi pÃ¤ivitetty":lang==="sv"?"JÃ¤mfÃ¶relse uppdaterad":"Benchmark updated",s:"bench"}
          ].map((a,i)=>
            <div key={i} className="portal-ar"><span className="portal-ad">{a.d}</span><span className="portal-at">{a.t}</span><span className={"portal-as "+a.s}>{a.s==="report"?(lang==="fi"?"Raportti":lang==="sv"?"Rapport":"Report"):a.s==="insight"?"WhatsApp":a.s==="fee"?(lang==="fi"?"Maksu":lang==="sv"?"Avgift":"Fee"):(lang==="fi"?"Vertailu":lang==="sv"?"JÃ¤mfÃ¶relse":"Bench")}</span></div>)}
        </div>}
        {tab==="proposals"&&<div>
          <div className="portal-ph">{lang==="fi"?"12 tarjousta vastaanotettu":lang==="sv"?"12 fÃ¶rslag mottagna":"12 proposals received"}</div>
          {[{b:"Lombard Odier",l:"Geneva",f:"0.70%",s:"selected"},{b:"Julius BÃ¤r",l:"Zurich",f:"0.75%",s:"reviewed"},{b:"Pictet",l:"Geneva",f:"0.65%",s:"reviewed"},{b:"EFG International",l:"Luxembourg",f:"0.80%",s:"meeting"},{b:"VP Bank",l:"Vaduz",f:"0.60%",s:"pending"}].map((p,i)=>
            <div key={i} className="portal-pr"><div><strong>{p.b}</strong><br/><span style={{fontSize:11,color:"#999"}}>{p.l}</span></div><div style={{fontWeight:600}}>{p.f}</div><div className={"portal-ps "+p.s}>{p.s==="selected"?(lang==="fi"?"Valittu":lang==="sv"?"Vald":"Selected"):p.s==="reviewed"?(lang==="fi"?"Tarkasteltu":lang==="sv"?"Granskad":"Reviewed"):p.s==="meeting"?(lang==="fi"?"Tapaaminen":lang==="sv"?"MÃ¶te":"Meeting"):(lang==="fi"?"Odottaa":lang==="sv"?"VÃ¤ntande":"Pending")}</div></div>)}
        </div>}
        {tab==="reports"&&<div>{[
          {d:"Dec 2025",t:lang==="fi"?"Kuukausiraportti":lang==="sv"?"MÃ¥nadsrapport":"Monthly Report"},
          {d:"Nov 2025",t:lang==="fi"?"Kuukausiraportti":lang==="sv"?"MÃ¥nadsrapport":"Monthly Report"},
          {d:"Q3 2025",t:lang==="fi"?"NeljÃ¤nnesvuosikatsaus":lang==="sv"?"KvartalsÃ¶versikt":"Quarterly Review"},
          {d:"Oct 2025",t:lang==="fi"?"Kuukausiraportti":lang==="sv"?"MÃ¥nadsrapport":"Monthly Report"}
        ].map((r,i)=>
          <div key={i} className="portal-rr"><span style={{color:"#999",minWidth:70,fontSize:12}}>{r.d}</span><span style={{flex:1}}>{r.t}</span><span style={{color:"#4A8FD4",fontSize:12,cursor:"pointer",fontWeight:500}}>{lang==="fi"?"Lataa PDF":lang==="sv"?"Ladda ner PDF":"Download PDF"}</span></div>)}</div>}
        {tab==="meetings"&&<div>{[
          {d:"Jan 15, 2026",t:lang==="fi"?"Vuosikatsaus - Lombard Odier":lang==="sv"?"Ã…rlig genomgÃ¥ng - Lombard Odier":"Annual Review - Lombard Odier",tp:"Video"},
          {d:"Dec 3, 2025",t:lang==="fi"?"Tapaaminen - EFG International":lang==="sv"?"Introduktion - EFG International":"Introduction - EFG International",tp:lang==="fi"?"HenkilÃ¶kohtaisesti":lang==="sv"?"Personligen":"In-person"},
          {d:"Nov 18, 2025",t:lang==="fi"?"Tapaaminen - Pictet":lang==="sv"?"Introduktion - Pictet":"Introduction - Pictet",tp:"Video"}
        ].map((m,i)=>
          <div key={i} className="portal-mr"><span style={{color:"#999",minWidth:90,fontSize:12}}>{m.d}</span><span style={{flex:1}}>{m.t}</span><span style={{color:"#4A8FD4",fontSize:11}}>{m.tp}</span></div>)}</div>}
      </div>
      <div className="portal-ft">{lang==="fi"?"Esikatselu â€” tÃ¤ltÃ¤ asiakasportaalisi nÃ¤yttÃ¤Ã¤":lang==="sv"?"FÃ¶rhandsgranskning â€” sÃ¥ hÃ¤r ser din kundportal ut":"Preview â€” this is what your client portal looks like"}</div>
    </div>
  );
}

/* â•â•â• v17: QUARTERLY REPORT â€” full FT-style with deep analysis â•â•â• */
function QReport({lang}){
  const alloc_total=ALLOC.reduce((s,a)=>s+a.v,0);
  const t = lang==="fi" ? {
    tag:"NeljÃ¤nnesvuosikatsaus", date:"Q4 2025 Â· Lokaâ€“Joulukuu", portVal:"Salkun arvo",
    ytd:"Vuoden alusta", q4:"Q4", peerRank:"Vertailussa", allInCost:"Kokonaiskulut",
    vsBench:"vs. Oikea vertailuindeksi", mgrFee:"Hoitopalkkio", execSum:"Yhteenveto",
    execText:"Suomalainen pankkisi raportoi: salkkusi tuotti +8,2% voittaen heidÃ¤n vertailuindeksinsÃ¤ +6,0%. NÃ¤yttÃ¤Ã¤ hyvÃ¤ltÃ¤. Mutta pankin valitsema vertailuindeksi on harhaanjohtava. Salkkusi on 42% osakkeita, 28% joukkovelkakirjoja, 12% kiinteistÃ¶jÃ¤ â€” kuitenkin pankki vertaa sinua 80% korkoihin painottuneeseen indeksiin. Miksi? Koska se on helppo voittaa. Kun rakensimme oikean vertailuindeksin (60% MSCI Europe, 30% EUR joukkovelkakirjat, 10% kiinteistÃ¶t), totuus paljastui: salkkusi on -9,8 prosenttiyksikkÃ¶Ã¤ jÃ¤ljessÃ¤. Olet maksanut salkunhoidosta mutta et tiennyt ettÃ¤ suoriutuminen on heikkoa. LisÃ¤ksi: kokonaiskulut 1,25% ylittÃ¤vÃ¤t vertaisryhmÃ¤n mediaanin 1,18%.",
    perf12:"Tuotto Â· 12 kuukautta", portfolio:"Salkku", benchmark:"Pankin vertailuindeksi",
    realBench:"Oikea vertailuindeksi", peerComp:"Vertaisvertailu", balanced:"Tasapainotettu",
    mandates:"mandaattia", yourReturn:"Sinun tuottosi", topQuart:"Ylin neljÃ¤nnes",
    peerMedian:"VertaisryhmÃ¤n mediaani", bottomQuart:"Alin neljÃ¤nnes",
    holdingsAnal:"Omistusanalyysi", holding:"Omistus", sector:"Sektori",
    weight:"Paino", contribution:"Kontribuutio"
  } : lang==="sv" ? {
    tag:"KvartalsÃ¶versikt", date:"Q4 2025 Â· Oktoberâ€“December", portVal:"PortfÃ¶ljvÃ¤rde",
    ytd:"Hittills i Ã¥r", q4:"Q4", peerRank:"JÃ¤mfÃ¶relse", allInCost:"Totalkostnad",
    vsBench:"vs. Korrekt jÃ¤mfÃ¶relseindex", mgrFee:"FÃ¶rvaltningsavgift", execSum:"Sammanfattning",
    execText:"Din finska bank rapporterade: din portfÃ¶lj levererade +8,2% och slog deras jÃ¤mfÃ¶relseindex pÃ¥ +6,0%. Ser bra ut. Men bankens valda jÃ¤mfÃ¶relseindex Ã¤r vilseledande. Din portfÃ¶lj Ã¤r 42% aktier, 28% obligationer, 12% fastigheter â€” Ã¤ndÃ¥ jÃ¤mfÃ¶r banken dig mot ett index tungt viktat mot 80% obligationer. VarfÃ¶r? FÃ¶r att det Ã¤r lÃ¤tt att slÃ¥. NÃ¤r vi konstruerade korrekt jÃ¤mfÃ¶relseindex (60% MSCI Europe, 30% EUR obligationer, 10% fastigheter) avslÃ¶jades sanningen: din portfÃ¶lj ligger -9,8 procentenheter efter. Du har betalat fÃ¶r fÃ¶rvaltning men visste inte att prestationen Ã¤r svag. Dessutom: totalkostnader pÃ¥ 1,25% Ã¶versteg medianvÃ¤rdet pÃ¥ 1,18%.",
    perf12:"Avkastning Â· 12 mÃ¥nader", portfolio:"PortfÃ¶lj", benchmark:"Bankens jÃ¤mfÃ¶relseindex",
    realBench:"Korrekt jÃ¤mfÃ¶relseindex", peerComp:"JÃ¤mfÃ¶relse med motsvarande", balanced:"Balanserad",
    mandates:"mandat", yourReturn:"Din avkastning", topQuart:"HÃ¶gsta kvartilen",
    peerMedian:"MedianvÃ¤rde", bottomQuart:"LÃ¤gsta kvartilen",
    holdingsAnal:"Innehavaanalys", holding:"Innehav", sector:"Sektor",
    weight:"Vikt", contribution:"Bidrag"
  } : {
    tag:"Quarterly Review", date:"Q4 2025 Â· October â€“ December", portVal:"Portfolio Value",
    ytd:"YTD", q4:"Q4", peerRank:"Peer Ranking", allInCost:"All-in Cost",
    vsBench:"vs Proper Benchmark", mgrFee:"Manager Fee", execSum:"Executive Summary",
    execText:"Your Finnish bank reported: your portfolio delivered +8.2%, beating their benchmark of +6.0%. Looks good. But the bank's chosen benchmark is misleading. Your portfolio is 42% equities, 28% bonds, 12% real estate â€” yet the bank compares you against an index heavily weighted to 80% bonds. Why? Because it's easy to beat. When we constructed the proper benchmark (60% MSCI Europe, 30% EUR bonds, 10% real estate), the truth emerged: your portfolio is -9.8 percentage points behind. You've been paying for management but didn't know performance was weak. Additionally: all-in costs at 1.25% exceeded peer median of 1.18%.",
    perf12:"Performance Â· 12 Months", portfolio:"Portfolio", benchmark:"Bank's Benchmark",
    realBench:"Proper Benchmark", peerComp:"Peer Comparison", balanced:"Balanced",
    mandates:"mandates", yourReturn:"Your Return", topQuart:"Top Quartile",
    peerMedian:"Peer Median", bottomQuart:"Bottom Quartile",
    holdingsAnal:"Holdings Analysis", holding:"Holding", sector:"Sector",
    weight:"Weight", contribution:"Contribution"
  };
  return(
    <div className="qr">
      <div className="qr-masthead"><div className="qr-mast-left"><span className="qr-mast-tag">{t.tag}</span><span className="qr-mast-date">{t.date}</span></div><span className="qr-mast-id">AU-2025-0847</span></div>
      <div className="qr-hero"><div className="qr-hero-left"><div className="qr-hero-label">{t.portVal}</div><div className="qr-hero-val">{"\u20AC2,164,000"}</div><div className="qr-hero-chg green">+8.2% {t.ytd} Â· +2.8% {t.q4}</div></div>
        <div className="qr-hero-kpis">{[{v:"Top 40%",l:t.peerRank},{v:"1.25%",l:t.allInCost},{v:"-9.8pp",l:t.vsBench},{v:"0.70%",l:t.mgrFee}].map((k,i)=>
          <div key={i} className="qr-hero-kpi"><div className="qr-hero-kv">{k.v}</div><div className="qr-hero-kl">{k.l}</div></div>)}</div></div>

      {/* Executive Summary */}
      <div className="qr-section"><div className="qr-sh">{t.execSum}</div>
        <div className="qr-prose">{t.execText}</div></div>

      {/* Performance chart */}
      <div className="qr-section"><div className="qr-sh">{t.perf12}</div>
        <ResponsiveContainer width="100%" height={180}>
          <AreaChart data={PORT_H} margin={{top:4,right:4,bottom:0,left:-20}}>
            <defs><linearGradient id="gQp" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stopColor="#0D4F8B" stopOpacity={0.1}/><stop offset="100%" stopColor="#0D4F8B" stopOpacity={0}/></linearGradient></defs>
            <CartesianGrid strokeDasharray="3 3" stroke="#E8E5E0" vertical={false}/>
            <XAxis dataKey="m" tick={{fontSize:9,fill:"#999"}} axisLine={false} tickLine={false}/>
            <YAxis tick={{fontSize:9,fill:"#999"}} axisLine={false} tickLine={false} tickFormatter={v=>v+"K"} domain={['dataMin-5','dataMax+5']}/>
            <Area type="monotone" dataKey="v" stroke="#0D4F8B" strokeWidth={2} fill="url(#gQp)"/>
            <Area type="monotone" dataKey="b" stroke="#C9975C" strokeWidth={1.2} fill="none" strokeDasharray="4 3"/>
            <Area type="monotone" dataKey="rb" stroke="#27AE60" strokeWidth={1.5} fill="none" strokeDasharray="2 2"/>
          </AreaChart>
        </ResponsiveContainer>
        <div className="qr-chart-leg"><span className="qr-leg"><span className="rp-dot" style={{background:"#0D4F8B"}}/>{t.portfolio} +8.2%</span><span className="qr-leg"><span className="rp-dot" style={{background:"#C9975C"}}/>{t.benchmark} +6.0%</span><span className="qr-leg"><span className="rp-dot" style={{background:"#27AE60"}}/>{t.realBench} +18.0%</span></div></div>

      {/* Peer Comparison */}
      <div className="qr-section"><div className="qr-sh">{t.peerComp} Â· {t.balanced} {"\u20AC1\u20135M"} (127 {t.mandates})</div>
        <div className="qr-peer-grid">
          {[{l:t.yourReturn,v:"+8.2%",bar:45,c:"#0D4F8B"},{l:t.topQuart,v:"+14.2%",bar:78,c:"#3DAA6D"},{l:t.peerMedian,v:"+11.2%",bar:61,c:"#C9975C"},{l:t.benchmark,v:"+6.0%",bar:33,c:"#999"},{l:t.bottomQuart,v:"+7.8%",bar:43,c:"#D4845A"}].map((p,i)=>
          <div key={i} className="qr-peer-row"><span className="qr-peer-label">{p.l}</span><div className="qr-peer-bar-wrap"><div className="qr-peer-bar" style={{width:p.bar+"%",background:p.c}}/></div><span className={"qr-peer-val"+(i===0?" bold":"")}>{p.v}</span></div>)}
        </div></div>

      {/* Holdings Deep-Dive */}
      <div className="qr-section"><div className="qr-sh">{t.holdingsAnal}</div>
        <div className="mr-tbl">
          <div className="mr-tbl-hdr qr-tbl-hdr"><span className="mr-th" style={{flex:2}}>{t.holding}</span><span className="mr-th">{t.sector}</span><span className="mr-th r">{t.weight}</span><span className="mr-th r">{t.ytd}</span><span className="mr-th r">{t.contribution}</span></div>
          {HOLDINGS.map((h,i)=><div key={i} className={"mr-tbl-row qr-tbl-row"+(i%2===0?" alt":"")}>
            <span className="mr-td" style={{flex:2,fontWeight:500}}>{h.n}</span>
            <span className="mr-td mr-td-sec">{translateSector(h.sec,lang)}</span>
            <span className="mr-td r">{h.w}</span>
            <span className={"mr-td r "+(h.ytd.startsWith("-")?"red":"grn")}>{h.ytd}</span>
            <span className={"mr-td r "+(h.cont.startsWith("-")?"red":"grn")}>{h.cont}</span>
          </div>)}
        </div></div>

      {/* Allocation + Currency */}
      <div className="qr-section"><div className="qr-sh">Asset Allocation & Currency</div>
        <div className="mr-two-col">
          <div className="mr-col">
            <div className="rp-stack-bar" style={{height:14,marginBottom:8}}>{ALLOC.map((a,i)=><div key={i} className="rp-stack-seg" style={{width:(a.v/alloc_total*100)+"%",background:a.c}} title={a.n}/>)}</div>
            <div className="mr-alloc-list">{ALLOC.map((a,i)=><div key={i} className="mr-alloc-item"><span className="rp-dot" style={{background:a.c}}/><span className="mr-alloc-name">{a.n}</span><span className="mr-alloc-pct">{a.v}%</span></div>)}</div>
          </div>
          <div className="mr-col">
            <div className="mr-ccy-list">{CCY.map((c,i)=><div key={i} className="mr-ccy-item"><div className="mr-ccy-bar-wrap"><div className="mr-ccy-bar" style={{width:c.w,background:c.clr}}/></div><span className="mr-ccy-code">{c.c}</span><span className="mr-ccy-pct">{c.w}</span></div>)}</div>
          </div>
        </div></div>

      {/* Risk Metrics */}
      <div className="qr-section"><div className="qr-sh">Risk Metrics</div>
        <div className="qr-risk-grid">
          {[{l:"Volatility (ann.)",v:"8.2%",ref:"Moderate",n:"Below peer avg 9.1%"},{l:"Sharpe Ratio",v:"1.42",ref:"Strong",n:"Above peer avg 1.15"},{l:"Max Drawdown",v:"-7.8%",ref:"Apr 2025",n:"Recovered in 5 weeks"},{l:"Beta to MSCI Europe",v:"0.72",ref:"Defensive",n:"Less market-sensitive"},{l:"Sortino Ratio",v:"1.89",ref:"Excellent",n:"Strong downside control"},{l:"Tracking Error",v:"3.4%",ref:"Active",n:"Meaningful active management"}].map((r,i)=>
          <div key={i} className="qr-risk-item"><div className="qr-risk-top"><span className="qr-risk-val">{r.v}</span><span className="qr-risk-ref">{r.ref}</span></div><div className="qr-risk-label">{r.l}</div><div className="qr-risk-note">{r.n}</div></div>)}
        </div></div>

      {/* Fee Summary */}
      <div className="qr-section"><div className="qr-sh">Cost Summary</div>
        <div className="qr-fee-compact">
          <div className="qr-fee-main"><span>All-in cost</span><span className="qr-fee-big">1.25%</span><span className="qr-fee-vs">vs peer median 1.17%</span></div>
          <div className="qr-fee-line-items">Bank 0.70% {"\u00B7"} Custody 0.10% {"\u00B7"} Transactions 0.15% {"\u00B7"} Funds 0.20% {"\u00B7"} <span className="mr-fee-au">Aureum 0.10%</span></div>
          <div className="mr-fee-selling">{"\u2713"} No hidden fees {"\u00B7"} No commissions {"\u00B7"} No kickbacks</div>
        </div></div>

      {/* Monte Carlo */}
      <div className="qr-section"><div className="qr-sh">Monte Carlo Projection Â· 20 Years</div>
        <div className="qr-mc-note">10,000 simulations based on current allocation, historical return distributions, and mean-reverting assumptions.</div>
        <ResponsiveContainer width="100%" height={200}>
          <AreaChart data={MC_DATA} margin={{top:4,right:4,bottom:0,left:-10}}>
            <defs>
              <linearGradient id="gMc95" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stopColor="#0D4F8B" stopOpacity={0.06}/><stop offset="100%" stopColor="#0D4F8B" stopOpacity={0}/></linearGradient>
              <linearGradient id="gMc75" x1="0" y1="0" x2="0" y2="1"><stop offset="0%" stopColor="#0D4F8B" stopOpacity={0.1}/><stop offset="100%" stopColor="#0D4F8B" stopOpacity={0.02}/></linearGradient>
            </defs>
            <CartesianGrid strokeDasharray="3 3" stroke="#E8E5E0" vertical={false}/>
            <XAxis dataKey="y" tick={{fontSize:9,fill:"#999"}} axisLine={false} tickLine={false} tickFormatter={v=>"Yr "+v}/>
            <YAxis tick={{fontSize:9,fill:"#999"}} axisLine={false} tickLine={false} tickFormatter={v=>v>=1000?(v/1000).toFixed(0)+"M":v+"K"}/>
            <Area type="monotone" dataKey="p95" stroke="none" fill="url(#gMc95)"/>
            <Area type="monotone" dataKey="p75" stroke="none" fill="url(#gMc75)"/>
            <Area type="monotone" dataKey="p50" stroke="#0D4F8B" strokeWidth={2} fill="none"/>
            <Area type="monotone" dataKey="p25" stroke="#C9975C" strokeWidth={1} fill="none" strokeDasharray="3 3"/>
            <Area type="monotone" dataKey="p5" stroke="#D4845A" strokeWidth={1} fill="none" strokeDasharray="2 4"/>
          </AreaChart>
        </ResponsiveContainer>
        <div className="qr-mc-bands">{[{c:"#0D4F8B",l:"Median (50th)",v:"\u20AC"+Math.round(MC_DATA[20].p50/1000).toFixed(0)+"M"},{c:"#C9975C",l:"25th pctl",v:"\u20AC"+Math.round(MC_DATA[20].p25/1000).toFixed(0)+"M"},{c:"#D4845A",l:"5th pctl (stress)",v:"\u20AC"+(MC_DATA[20].p5/1000).toFixed(1)+"M"}].map((b,i)=>
          <span key={i} className="qr-mc-band"><span className="rp-dot" style={{background:b.c}}/>{b.l}: <strong>{b.v}</strong></span>)}</div></div>

      {/* Stress Test */}
      <div className="qr-section"><div className="qr-sh">Stress Test Scenarios</div>
        <div className="qr-prose qr-prose-sm" style={{marginBottom:10}}>How would your current portfolio have performed during major historical market events?</div>
        <div className="qr-stress">{STRESS.map((s,i)=>(
          <div key={i} className="qr-stress-row"><div className="qr-stress-name">{s.sc}</div>
            <div className="qr-stress-vals">
              <span className="qr-sv red">{s.eq>0?"+":""}{s.eq}%<span className="qr-svl">Equity</span></span>
              <span className={"qr-sv "+(s.fi>=0?"grn":"red")}>{s.fi>0?"+":""}{s.fi}%<span className="qr-svl">Fixed Inc</span></span>
              <span className="qr-sv red">{s.tot}%<span className="qr-svl">Portfolio</span></span>
              <span className="qr-sv">{s.rec}<span className="qr-svl">Recovery</span></span>
            </div></div>))}</div></div>

      {/* Aureum Actions & Recommendations */}
      <div className="qr-section"><div className="qr-sh">Aureum Observations</div>
        <div className="qr-actions">
          {[{icon:"\u2713",t:"Performance: strong",d:"Your manager outperformed the composite benchmark by 5.1pp. Consistency across three of four quarters this year."},{icon:"\u26A0",t:"Fee review recommended",d:"Management fee 5bps above peer median. We suggest requesting a fee review at the January annual meeting given the relationship tenure."},{icon:"\u2139",t:"Currency note",d:"USD exposure at 24%. If you expect EUR/USD to mean-revert, consider discussing a partial hedge with your manager."},{icon:"\u2713",t:"Risk controls adequate",d:"Max drawdown -7.8% within the agreed -10% threshold. Volatility below peer average indicates conservative positioning."}].map((a,i)=>
          <div key={i} className="qr-action"><span className={"qr-action-icon"+(a.icon==="\u26A0"?" warn":"")}>{a.icon}</span><div><div className="qr-action-t">{a.t}</div><div className="qr-action-d">{a.d}</div></div></div>)}
        </div></div>

      <div className="qr-disc">This material is for informational purposes only and does not constitute investment advice. Monte Carlo simulations use historical data and do not predict future performance. Past performance is not indicative of future results. Prepared by Aureum Private Office under power of attorney.</div>
    </div>
  );
}

/* â•â•â• v16: BENCHMARK VISUALIZATION â•â•â• */
function BenchmarkViz(){
  const[view,setView]=useState("before");
  const d=view==="before"?BENCH_BEFORE:BENCH_AFTER;
  return(
    <div className="bv">
      <div className="bv-tabs"><button className={"bv-tab"+(view==="before"?" on":"")} onClick={()=>setView("before")}>Bank's Benchmark</button><button className={"bv-tab"+(view==="after"?" on":"")} onClick={()=>setView("after")}>Proper Benchmark</button></div>
      <div className="bv-chart">
        <ResponsiveContainer width="100%" height={160}>
          <AreaChart data={d} margin={{top:4,right:4,bottom:0,left:-20}}>
            <CartesianGrid strokeDasharray="3 3" stroke="#1A3258" vertical={false}/>
            <XAxis dataKey="m" tick={{fontSize:9,fill:"#637896"}} axisLine={false} tickLine={false}/>
            <YAxis tick={{fontSize:9,fill:"#637896"}} axisLine={false} tickLine={false} domain={['dataMin-3','dataMax+3']}/>
            <Area type="monotone" dataKey="p" stroke="#4A8FD4" strokeWidth={2} fill="none" name="Portfolio"/>
            <Area type="monotone" dataKey="b" stroke={view==="before"?"#C9975C":"#27AE60"} strokeWidth={1.5} fill="none" strokeDasharray="4 3" name="Benchmark"/>
          </AreaChart>
        </ResponsiveContainer>
        <div className="bv-verdict">{view==="before"?<><span className="bv-good">{"\u2713"} Beating benchmark by +2.7%</span><span className="bv-exp">Bank chose 80% bond benchmark â€” easy to beat, hides true performance</span></>:<><span className="bv-bad">{"\u2717"} Trailing by -14.7%</span><span className="bv-exp">Proper benchmark (60% MSCI Europe, 30% EUR bonds, 10% real estate) shows reality</span></>}</div>
      </div>
    </div>
  );
}

/* â•â•â• v16: SERVICE DETAIL MODAL â•â•â• */
function ServiceDetail({svc,onClose,lang,onStart}){
  if(svc===null||svc===undefined) return null;
  const testimonials=[
    {q:"We had been with the same bank for twelve years. Aureum brought us 12 competing offers in two weeks â€” including three banks with Finnish-speaking relationship managers we didn't know existed.",who:"Technology entrepreneur, Luxembourg",aum:"\u20AC4.8M"},
    {q:"The monthly reports alone justify the fee. For the first time, I actually understand what my bank is charging me and how my portfolio is really performing.",who:"Real estate investor, Helsinki",aum:"\u20AC2.1M"},
    {q:"My previous bank chose benchmarks that made them look good. Aureum showed me the proper benchmark and revealed years of underperformance I never knew about.",who:"Business owner, Espoo",aum:"\u20AC3.5M"},
    {q:"I message them at 22:00 on a Sunday about a currency move. Ten minutes later I have a clear, sourced answer with how it affects my portfolio. That's not a service â€” that's a partner.",who:"Shipping executive, Turku",aum:"\u20AC6.2M"},
  ];
  const tm=testimonials[svc];
  return(
    <div className="fv-overlay" onClick={onClose}>
      <div className="fv-modal sd-modal" onClick={e=>e.stopPropagation()}>
        <div className="fv-header"><div className="fv-header-left"><Logo size={20}/><span className="fv-header-title">{[lang==="fi"?"Kilpailutus":lang==="sv"?"KonkurrensutsÃ¤ttning":"Competitive Sourcing",lang==="fi"?"RÃ¤Ã¤tÃ¤lÃ¶idyt raportit":lang==="sv"?"SkrÃ¤ddarsydda rapporter":"Bespoke Reporting",lang==="fi"?"Suoritusvertailu":lang==="sv"?"ResultatjÃ¤mfÃ¶relse":"Performance Benchmarking","WhatsApp Insights"][svc]}</span></div>
          <button className="fv-close" onClick={onClose}>{"\u2715"}</button></div>
        <div className="fv-body sd-body">
          {/* Testimonial */}
          <div className="sd-test"><div className="sd-test-q">{"\u201C"}{tm.q}{"\u201D"}</div><div className="sd-test-who">{"\u2014 "}{tm.who} Â· {tm.aum}</div></div>

          {svc===0&&<div className="sd-content">
            <p className="sd-intro">{lang==="fi"?"LÃ¤hetÃ¤mme anonymisoidun profiilisi jopa 15 kilpailevalle pankille verkostostamme, jossa on yli 25 pankkia ja vakuutuskuoripalveluntarjoajaa. Saat strukturoidut tarjoukset, vertailet ehtoja rinnakkain ja tapaat pankkiirit jotka vastaavat kieltÃ¤si ja sijoitustyyliÃ¤si. SinÃ¤ pÃ¤Ã¤tÃ¤t â€” me helpotamme.":lang==="sv"?"Vi skickar din anonymiserade profil till upp till 15 konkurrerande banker utvalda frÃ¥n vÃ¥rt nÃ¤tverk av 25+ banker och fÃ¶rsÃ¤kringsskydd-leverantÃ¶rer. Du fÃ¥r strukturerade fÃ¶rslag, jÃ¤mfÃ¶r villkor sida vid sida och trÃ¤ffar bankirer som matchar ditt sprÃ¥k och investeringsstil. Du bestÃ¤mmer â€” vi underlÃ¤ttar.":"We send your anonymized profile to up to 15 competing banks selected from our network of 25+ banks and insurance wrapper providers. You receive structured proposals, compare terms side by side, and meet the bankers who match your language and investment style. You decide â€” we facilitate."}</p>
            <div className="sd-sh">{lang==="fi"?"Pohjoismaiset varainhoitajat":lang==="sv"?"Nordiska fÃ¶rmÃ¶genhetsfÃ¶rvaltare":"Nordic Wealth Managers"}</div>
            <div className="sd-banks">{BANKS_NORDIC.map((b,i)=><div key={i} className="sd-bank"><div className="sd-bank-top"><div><div className="sd-bank-name">{b.n}</div><div className="sd-bank-loc">Min {b.min} Â· {b.lang}</div></div></div><div className="sd-bank-spec">{b.spec}</div></div>)}</div>
            <div className="sd-sh">{lang==="fi"?"KansainvÃ¤liset yksityispankit":lang==="sv"?"Internationella privatbanker":"International Private Banks"}</div>
            <div className="sd-banks">{BANKS_INTL.map((b,i)=><div key={i} className="sd-bank"><div className="sd-bank-top"><div><div className="sd-bank-name">{b.n}</div><div className="sd-bank-loc">Min {b.min} Â· {b.lang}</div></div></div><div className="sd-bank-spec">{b.spec}</div></div>)}</div>
          </div>}

          {svc===1&&<div className="sd-content">
            <p className="sd-intro">{lang==="fi"?"Rajoitetun valtakirjan nojalla pankkisi lÃ¤hettÃ¤Ã¤ meille sÃ¤Ã¤nnÃ¶lliset salkkuraportit. Muunnamme raa'an pankkidatan selkeiksi, visuaalisiksi yhteenvedoiksi â€” suunniteltu niin, ettÃ¤ ymmÃ¤rrÃ¤t varallisuutesi minuuteissa, et tunneissa. Saatavilla suomeksi, ruotsiksi tai englanniksi.":lang==="sv"?"Under en begrÃ¤nsad fullmakt skickar din bank oss periodiska portfÃ¶ljrapporter. Vi fÃ¶rvandlar rÃ¥ bankdata till tydliga, visuella sammanfattningar â€” designade sÃ¥ att du fÃ¶rstÃ¥r din fÃ¶rmÃ¶genhet pÃ¥ minuter, inte timmar. TillgÃ¤nglig pÃ¥ finska, svenska eller engelska.":"Under a limited power of attorney, your bank sends us periodic portfolio reports. We transform raw bank data into clear, visual summaries â€” designed so you understand your wealth in minutes, not hours. Available in Finnish, Swedish, or English."}</p>
            <div className="sd-sh">{lang==="fi"?"Kuukausiraportti":lang==="sv"?"MÃ¥nadsrapport":"Monthly Report"}</div>
            <div className="sd-report-frame"><RPV lang={lang}/></div>
            <div className="sd-sh">{lang==="fi"?"NeljÃ¤nnesvuosikatsaus":lang==="sv"?"KvartalsÃ¶versikt":"Quarterly Review"}</div>
            <div className="sd-report-frame"><QReport lang={lang}/></div>
          </div>}

          {svc===2&&<div className="sd-content">
            <p className="sd-intro">{lang==="fi"?"Useimmille asiakkaille ei ole koskaan nÃ¤ytetty miten heidÃ¤n salkunhoitajansa todella suoriutuu. Pankit raportoivat absoluuttisia tuottoja â€” mutta eivÃ¤t koskaan nÃ¤ytÃ¤ mitÃ¤ vertailukelpoinen passiivinen salkku olisi tuottanut. Me muutamme tÃ¤mÃ¤n.":lang==="sv"?"De flesta kunder har aldrig fÃ¥tt se hur deras fÃ¶rvaltare faktiskt presterar. Banker rapporterar absolut avkastning â€” men visar aldrig vad en jÃ¤mfÃ¶rbar passiv portfÃ¶lj skulle ha levererat. Vi Ã¤ndrar det.":"Most clients have never been shown how their manager actually performs. Banks report absolute returns â€” but never show you what a comparable passive portfolio would have delivered. We change that."}</p>
            <div className="sd-sh">{lang==="fi"?"Vertailuindeksin ongelma":lang==="sv"?"JÃ¤mfÃ¶relseindexproblemet":"The Benchmark Problem"}</div>
            <div className="sd-story">
              <p>{lang==="fi"?"HelsinkilÃ¤inen yritysomistaja tuli Aureumille tasapainotettua salkkua hoitavasta suomalaisesta pankista. HÃ¤nen vuosikatsauksensa nÃ¤ytti +8,2% tuottoa ja pankkiiri kehui: \"Erinomaista! Voititte vertailuindeksimme joka tuotti +6,0%.\". Asiakas oli tyytyvÃ¤inen.":lang==="sv"?"En Helsingforsbaserad fÃ¶retagsÃ¤gare kom till Aureum med en balanserad portfÃ¶lj hos en finsk bank. Hans Ã¥rliga Ã¶versikt visade +8,2% avkastning och bankiren berÃ¶mde: \"UtmÃ¤rkt! Ni slog vÃ¥rt jÃ¤mfÃ¶relseindex pÃ¥ +6,0%\". Kunden var nÃ¶jd.":"A Helsinki-based business owner came to Aureum with a balanced portfolio at a Finnish bank. His annual review showed +8.2% returns and the banker praised: \"Excellent! You beat our benchmark of +6.0%\". The client was pleased."}</p>
              <p>{lang==="fi"?"Teimme riippumattoman analyysin. HÃ¤nen pankkinsa oli valinnut erittÃ¤in konservatiivisen vertailuindeksin â€” 80% joukkovelkakirjoja, 20% osakkeita. Miksi? Koska tÃ¤llainen indeksi on helppo voittaa. HÃ¤nen todellinen salkkunsa oli 42% osakkeita, 28% joukkovelkakirjoja, 12% kiinteistÃ¶jÃ¤.":lang==="sv"?"Vi gjorde en oberoende analys. Hans bank hade valt ett extremt konservativt jÃ¤mfÃ¶relseindex â€” 80% obligationer, 20% aktier. VarfÃ¶r? FÃ¶r att ett sÃ¥dant index Ã¤r lÃ¤tt att slÃ¥. Hans verkliga portfÃ¶lj var 42% aktier, 28% obligationer, 12% fastigheter.":"We ran an independent analysis. His bank had chosen an extremely conservative benchmark â€” 80% bonds, 20% equities. Why? Because such an index is easy to beat. His actual portfolio was 42% equities, 28% bonds, 12% real estate."}</p>
              <p>{lang==="fi"?"Kun rakensimme oikean vertailuindeksin hÃ¤nen todelliseen allokaatioonsa â€” 60% MSCI Europe, 30% EUR joukkovelkakirjat, 10% kiinteistÃ¶t â€” totuus paljastui. Oikea vertailuindeksi tuotti +18,0%. HÃ¤nen salkkuÐ½ oli -9,8 prosenttiyksikkÃ¶Ã¤ jÃ¤ljessÃ¤. Pankki piilotti merkittÃ¤vÃ¤n alisuoriutumisen valitsemalla vÃ¤Ã¤rÃ¤n vertailuindeksin.":lang==="sv"?"NÃ¤r vi konstruerade korrekt jÃ¤mfÃ¶relseindex fÃ¶r hans verkliga allokering â€” 60% MSCI Europe, 30% EUR obligationer, 10% fastigheter â€” avslÃ¶jades sanningen. Korrekt jÃ¤mfÃ¶relseindex gav +18,0%. Hans portfÃ¶lj lÃ¥g -9,8 procentenheter efter. Banken dolde betydande underprestation genom att vÃ¤lja fel jÃ¤mfÃ¶relseindex.":"When we constructed the proper benchmark for his actual allocation â€” 60% MSCI Europe, 30% EUR bonds, 10% real estate â€” the truth emerged. The proper benchmark returned +18.0%. His portfolio was -9.8 percentage points behind. The bank had hidden significant underperformance by choosing the wrong benchmark."}</p>
              <p>{lang==="fi"?"HÃ¤n maksoi salkunhoidosta mutta ei tiennyt ettÃ¤ suoriutuminen oli heikkoa. LisÃ¤ksi huomasimme, ettÃ¤ hÃ¤nen palkkionsa olivat 0,55% vertaisryhmÃ¤n mediaanin ylÃ¤puolella. PelkÃ¤stÃ¤Ã¤n tuo keskustelu sÃ¤Ã¤styi hÃ¤nelle yli 18 000â‚¬ vuodessa.":lang==="sv"?"Han betalade fÃ¶r fÃ¶rvaltning men visste inte att prestationen var svag. Dessutom upptÃ¤ckte vi att hans avgifter var 0,55% Ã¶ver medianvÃ¤rdet. Enbart det samtalet sparade honom Ã¶ver 18 000â‚¬ per Ã¥r.":"He was paying for management but didn't know performance was weak. Additionally, we found his fees were 0.55% above the peer median. That conversation alone saved him over â‚¬18,000 per year."}</p>
            </div>
            <BenchmarkViz/>
            <div className="sd-sh">{lang==="fi"?"MitÃ¤ saat":lang==="sv"?"Vad du fÃ¥r":"What You Get"}</div>
            <div className="sd-features">{(lang==="fi"?["RÃ¤Ã¤tÃ¤lÃ¶ity yhdistelmÃ¤vertailuindeksi todelliseen allokaatioosi sopivaksi","NeljÃ¤nnesvuosittainen vertaisvertailu vertailukelpoisiin mandaatteihin","Kuluanalyysi vs. markkinan mediaani â€” eritelty komponenteittain","HÃ¤lytys jos salkunhoitajasi alisuoriutuu kahden perÃ¤kkÃ¤isen neljÃ¤nneksen ajan"]:lang==="sv"?["Anpassat sammansatt jÃ¤mfÃ¶relseindex matchat till din faktiska allokering","Kvartalsvis jÃ¤mfÃ¶relse med motsvarande mandat","Avgiftsanalys vs marknadsmedian â€” uppdelat per komponent","Varning om din fÃ¶rvaltare underpresterar tvÃ¥ kvartal i rad"]:["Custom composite benchmark matched to your actual allocation","Quarterly peer comparison across comparable mandates","Fee analysis vs market median â€” broken down by component","Alert if your manager underperforms for two consecutive quarters"]).map((f,i)=><div key={i} className="sd-feat"><span className="sd-feat-dot"/>{f}</div>)}</div>
          </div>}

          {svc===3&&<div className="sd-content">
            <p className="sd-intro">{lang==="fi"?"Salkkusi ei lopeta liikkumista kun markkinat sulkeutuvat. Me emme myÃ¶skÃ¤Ã¤n. Viestit meille milloin tahansa WhatsAppissa â€” kysy markkinoista, omistuksistasi, valuuttaliikkeistÃ¤ tai mistÃ¤ tahansa muusta. Vastaamme todellisella datalla, joka on perÃ¤isin viimeisimmistÃ¤ raporteistasi.":lang==="sv"?"Din portfÃ¶lj slutar inte rÃ¶ra sig nÃ¤r marknaderna stÃ¤nger. Det gÃ¶r inte heller vi. Skicka meddelande till oss nÃ¤r som helst pÃ¥ WhatsApp â€” frÃ¥ga om marknader, dina innehav, valutarÃ¶relser eller nÃ¥got annat. Vi svarar med verklig data, hÃ¤mtad frÃ¥n dina senaste rapporter.":"Your portfolio doesn't stop moving when markets close. Neither do we. Message us anytime on WhatsApp â€” ask about markets, your holdings, currency moves, or anything else. We respond with real data, sourced from your latest reports."}</p>
            <div className="sd-sh">{lang==="fi"?"Todellinen keskustelu":lang==="sv"?"En verklig konversation":"A Real Conversation"}</div>
            <div className="sd-wa-frame"><WAP/></div>
            <div className="sd-sh">{lang==="fi"?"MitÃ¤ voit kysyÃ¤":lang==="sv"?"Vad du kan frÃ¥ga":"What You Can Ask"}</div>
            <div className="sd-features">{(lang==="fi"?["MitÃ¤ tapahtui markkinoilla tÃ¤nÃ¤Ã¤n â€” ja miten se vaikuttaa minuun?","Miten salkkuni suoriutuu vertailuindeksiin nÃ¤hden tÃ¤ssÃ¤ kuussa?","MikÃ¤ on nykyinen valuuttajakaumani?","Voitko tiivistÃ¤Ã¤ viimeisimmÃ¤n kuukausiraporttini?","MitkÃ¤ ovat kokonaiskuluni vuoden alusta?","PitÃ¤isikÃ¶ minun olla huolissani [tietystÃ¤ markkinatapahtumasta]?"]:lang==="sv"?["Vad hÃ¤nde pÃ¥ marknaderna idag â€” och hur pÃ¥verkar det mig?","Hur presterar min portfÃ¶lj vs jÃ¤mfÃ¶relseindex denna mÃ¥nad?","Vad Ã¤r min nuvarande valutaexponering?","Kan du sammanfatta min senaste mÃ¥nadsrapport?","Vad Ã¤r mina totala avgifter hittills i Ã¥r?","BÃ¶r jag vara orolig fÃ¶r [specifik marknadshÃ¤ndelse]?"]:["What happened in markets today â€” and how does it affect me?","How is my portfolio performing vs benchmark this month?","What is my current currency exposure?","Can you summarize my latest monthly report?","What are my total fees year-to-date?","Should I be concerned about [specific market event]?"]).map((f,i)=><div key={i} className="sd-feat"><span className="sd-feat-dot"/>{f}</div>)}</div>
          </div>}

          <div className="sd-cta"><button className="btn-p" onClick={onStart}><span>{lang==="fi"?"Aloita prosessi":lang==="sv"?"Starta processen":"Start the Process"}</span><Arr/></button></div>
        </div>
      </div>
    </div>
  );
}

/* â•â•â• MAIN â•â•â• */
export default function Aureum(){
  const[kyc,setKyc]=useState(false);
  const[scr,setScr]=useState(false);
  const[lang,setLang]=useState("fi");
  const[mob,setMob]=useState(false);
  const[fullView,setFullView]=useState(null); // "report" | "portal" | null
  const[svcDetail,setSvcDetail]=useState(null); // 0-3 | null
  const[legal,setLegal]=useState(null); // "terms" | "privacy" | null
  const[article,setArticle]=useState(null); // 0|1|2 | null
  const[cookie,setCookie]=useState(true); // show cookie banner
  const t=T[lang];
  const mR=useRef(null);
  useEffect(()=>{if(!document.querySelector("link[data-auf]")){const l=document.createElement("link");l.rel="stylesheet";l.href=FU;l.setAttribute("data-auf","1");document.head.appendChild(l)}},[]);
  useEffect(()=>{
    if(document.querySelector("meta[data-au]"))return;
    const m=[
      {name:"description",content:"Independent wealth concierge. Up to 15 competing proposals from 25+ European private banks. Bespoke reporting, performance benchmarking, and banker matching in Finnish, Swedish, or English."},
      {property:"og:title",content:"Aureum Private Office â€” Independent Wealth Concierge"},
      {property:"og:description",content:"Better terms. Better reporting. Better informed. Source up to 15 proposals from 25+ European private banks. Fee-only and fully independent."},
      {property:"og:type",content:"website"},
      {property:"og:url",content:"https://aureumprivateoffice.com"},
      {property:"og:site_name",content:"Aureum Private Office"},
      {name:"twitter:card",content:"summary"},
      {name:"twitter:title",content:"Aureum Private Office â€” Independent Wealth Concierge"},
      {name:"twitter:description",content:"Source up to 15 competing proposals from 25+ European private banks. Fee-only, independent. 0% kickbacks."},
      {name:"robots",content:"index, follow"},
      {name:"author",content:"Aureum Private Office"},
      {name:"theme-color",content:"#0C1E3A"},
    ];
    m.forEach(a=>{const el=document.createElement("meta");Object.entries(a).forEach(([k,v])=>el.setAttribute(k,v));el.setAttribute("data-au","1");document.head.appendChild(el)});
    document.title="Aureum Private Office â€” Independent Wealth Concierge";
    if(!document.querySelector("link[rel='canonical']")){const c=document.createElement("link");c.rel="canonical";c.href="https://aureumprivateoffice.com";document.head.appendChild(c)}
    // JSON-LD structured data
    if(!document.querySelector("script[data-au-ld]")){
      const ld=document.createElement("script");ld.type="application/ld+json";ld.setAttribute("data-au-ld","1");
      ld.textContent=JSON.stringify({"@context":"https://schema.org","@type":"FinancialService","name":"Aureum Private Office","description":"Independent wealth concierge. Competitive sourcing from 25+ European private banks.","url":"https://aureumprivateoffice.com","founder":{"@type":"Person","name":"Noah Kraama"},"areaServed":["Finland","Luxembourg","Switzerland","United Kingdom","Singapore","UAE","Monaco"],"serviceType":"Wealth Concierge","priceRange":"From 0.05% annually"});
      document.head.appendChild(ld);
    }
  },[]);
  useEffect(()=>{const el=mR.current;if(!el)return;const h=()=>setScr(el.scrollTop>50);el.addEventListener("scroll",h,{passive:true});return()=>el.removeEventListener("scroll",h)},[]);
  // Section entrance animations
  useEffect(()=>{
    const el=mR.current;if(!el)return;
    const io=new IntersectionObserver((entries)=>{entries.forEach(e=>{if(e.isIntersecting)e.target.classList.add("vis")})},{root:el,threshold:0.08,rootMargin:"0px 0px -40px 0px"});
    el.querySelectorAll(".sec, .cta, .hero").forEach(s=>io.observe(s));
    return()=>io.disconnect();
  },[]);
  const go=(id)=>{const el=document.getElementById(id);if(el)el.scrollIntoView({behavior:"smooth"});setMob(false)};
  const navIds=["services","process","preview","founder","pricing"];

  return(<>
    <style>{CSS}</style>
    <div className="au">
      {/* NAV â€” v13: mobile hamburger */}
      <nav className={"nv"+(scr?" s":"")}><div className="nv-in">
        <div className="lg"><Logo size={26}/><div><div className="lg-t">Aureum</div><div className="lg-s">Private Office</div></div></div>
        <div className="nv-r nv-desk">
          {t.nav.slice(0,5).map((n,i)=><button key={i} className="nv-a" onClick={()=>go(navIds[i])}>{n}</button>)}
          <div className="lang-sw">{[{c:"fi",f:"ðŸ‡«ðŸ‡®"},{c:"en",f:"ðŸ‡¬ðŸ‡§"},{c:"sv",f:"ðŸ‡¸ðŸ‡ª"}].map(l=><button key={l.c} className={"lang-btn"+(lang===l.c?" on":"")} onClick={()=>setLang(l.c)} title={l.c==="fi"?"Suomeksi":l.c==="en"?"English":"Svenska"}>{l.f}</button>)}</div>
          <button className="nv-cta" onClick={()=>setKyc(true)}>{t.nav[5]}</button>
        </div>
        <div className="nv-r nv-mob">
          <div className="lang-sw">{[{c:"fi",f:"ðŸ‡«ðŸ‡®"},{c:"en",f:"ðŸ‡¬ðŸ‡§"},{c:"sv",f:"ðŸ‡¸ðŸ‡ª"}].map(l=><button key={l.c} className={"lang-btn"+(lang===l.c?" on":"")} onClick={()=>setLang(l.c)} title={l.c==="fi"?"Suomeksi":l.c==="en"?"English":"Svenska"}>{l.f}</button>)}</div>
          <button className="nv-burger" onClick={()=>setMob(v=>!v)}><Burger open={mob}/></button>
        </div>
      </div></nav>

      {/* MOBILE MENU */}
      {mob&&<div className="mob-ov" onClick={()=>setMob(false)}/>}
      <div className={"mob-menu"+(mob?" open":"")}>
        {t.nav.slice(0,5).map((n,i)=><button key={i} className="mob-a" onClick={()=>go(navIds[i])}>{n}</button>)}
        <button className="mob-cta" onClick={()=>{setMob(false);setKyc(true)}}>{t.nav[5]}</button>
      </div>

      <div className="mn" ref={mR}>
        {/* HERO â€” v13: animated geometric background */}
        <section className="hero"><HeroBG/><div className="hero-c">
          <div className="hero-lab">{t.hero_lab}</div>
          <h1 className="hero-h1">{t.hero_h[0]}<span className="gld">{t.hero_h[1]}</span>{t.hero_h[2]}</h1>
          <p className="hero-p">{t.hero_p}</p>
          <div className="hero-fq"><span className="hero-fq-text">{t.hero_fq}</span><span className="hero-fq-attr">{t.hero_fqa}</span></div>
          <div className="hero-acts"><button className="btn-p" onClick={()=>setKyc(true)}><span>{t.hero_cta[0]}</span><Arr/></button><button className="btn-g" onClick={()=>go("services")}>{t.hero_cta[1]}</button></div>
          <div className="hero-stats">
            <CountStat num={18} suffix="+" label={t.stats[0][1]}/>
            <CountStat num={0} suffix="%" label={t.stats[1][1]}/>
            <CountStat num={25} suffix="+" label={t.stats[2][1]}/>
            <CountStat num={15} prefix={lang==="fi"?"Jopa ":lang==="sv"?"Upp till ":"Up to "} label={t.stats[3][1]}/>
          </div>
        </div></section>

        {/* SERVICES â€” v16: clickable cards */}
        <section className="sec" id="services"><div className="sec-in">
          <div className="sec-lab">{t.svc_lab}</div><h2 className="sec-h2">{t.svc_h}</h2>
          <div className="svc4">{t.svcs.map((s,i)=><button key={i} className="svc svc-link" onClick={()=>setSvcDetail(i)}><div className="svc-i">{SVC_ICONS[i]}</div><h3 className="svc-t">{s[0]}</h3><p className="svc-d">{s[1]}</p><div className="svc-bot"><div className="svc-tag">{s[2]}</div><span className="svc-more">{lang==="fi"?"Lue lisÃ¤Ã¤":lang==="sv"?"LÃ¤s mer":"Learn more"} {"\u2192"}</span></div></button>)}</div>
        </div></section>

        {/* LANGUAGE â€” v30: clean with hover testimonials */}
        <section className="sec sec-alt" id="language"><div className="sec-in">
          <div className="sec-lab">{t.lang_lab}</div><h2 className="sec-h2">{t.lang_h}</h2>
          <p className="lang-hero-p">{t.lang_p1}</p>
          <div className="lang-cards">
            {t.langs.map((l,i)=>(
              <div key={i} className="lang-card">
                <div className="lang-card-icon">{FLAG_ICONS[i]}</div>
                <div className="lang-card-body">
                  <div className="lang-card-name">{l[0]}</div>
                  <div className="lang-card-desc">{l[1]}</div>
                </div>
                <div className="lang-tip">
                  <div className="lang-tip-quote">{l[2]}</div>
                  <div className="lang-tip-attr">{l[3]}</div>
                </div>
              </div>
            ))}
          </div>
        </div></section>

        {/* HOW IT WORKS */}
        <section className="sec" id="process"><div className="sec-in">
          <div className="sec-lab">{t.hw_lab}</div><h2 className="sec-h2">{t.hw_h}</h2>
          <div className="hw-steps">{t.steps.map((s,i)=><div key={i} className="hw-step"><div className="hw-n">{"0"+(i+1)}</div><h3 className="hw-t">{s[0]}</h3><p className="hw-d">{s[1]}</p><div className="hw-dur">{s[2]}</div></div>)}</div>
        </div></section>

        {/* v13: SOCIAL PROOF */}
        <section className="sec sec-alt" id="social-proof"><div className="sec-in">
          <div className="sec-lab">{t.sp_lab}</div><h2 className="sec-h2">{t.sp_h}</h2>
          <SocialProof t={t}/>
        </div></section>

        {/* PREVIEW â€” v15: compact preview cards with magic links */}
        <section className="sec" id="preview"><div className="sec-in">
          <div className="sec-lab">{t.prev_lab}</div><h2 className="sec-h2">{t.prev_h}</h2>
          <div className="pv-cards">
            <button className="pv-card" onClick={()=>setFullView("report")}>
              <div className="pv-card-inner">
                <div className="pv-card-header">
                  <div className="pv-card-icon">{"\u25A3"}</div>
                  <div><div className="pv-card-title">{lang==="fi"?"Kuukausiraportti":lang==="sv"?"MÃ¥nadsrapport":"Monthly Report"}</div>
                  <div className="pv-card-sub">{lang==="fi"?"Joulukuu 2025 Â· Lombard Odier":lang==="sv"?"December 2025 Â· Lombard Odier":"December 2025 Â· Lombard Odier"}</div></div>
                </div>
                <div className="pv-card-stats">
                  <div className="pv-card-stat"><span className="pv-cs-v">{"\u20AC2.16M"}</span><span className="pv-cs-l">{lang==="fi"?"Arvo":lang==="sv"?"VÃ¤rde":"Value"}</span></div>
                  <div className="pv-card-stat"><span className="pv-cs-v green">+8.2%</span><span className="pv-cs-l">YTD</span></div>
                  <div className="pv-card-stat"><span className="pv-cs-v gold">Top 40%</span><span className="pv-cs-l">{lang==="fi"?"Vertailu":lang==="sv"?"JÃ¤mfÃ¶relse":"Peers"}</span></div>
                </div>
                <div className="pv-card-cta">{lang==="fi"?"Avaa raportti":lang==="sv"?"Ã–ppna rapport":"View full report"} {"\u2192"}</div>
              </div>
            </button>
            <button className="pv-card" onClick={()=>setFullView("portal")}>
              <div className="pv-card-inner">
                <div className="pv-card-header">
                  <div className="pv-card-icon">{"\u25C8"}</div>
                  <div><div className="pv-card-title">{lang==="fi"?"Asiakasportaali":lang==="sv"?"Kundportal":"Client Portal"}</div>
                  <div className="pv-card-sub">{lang==="fi"?"Varallisuuden seuranta":lang==="sv"?"FÃ¶rmÃ¶genhetsÃ¶versikt":"Wealth monitoring dashboard"}</div></div>
                </div>
                <div className="pv-card-features">
                  {(lang==="fi"?["Salkkukatsaus","Tarjoukset","Raportit","Tapaamiset"]:lang==="sv"?["PortfÃ¶ljÃ¶versikt","FÃ¶rslag","Rapporter","MÃ¶ten"]:["Portfolio overview","Proposals","Reports","Meetings"]).map((f,i)=>
                    <span key={i} className="pv-card-feat">{f}</span>)}
                </div>
                <div className="pv-card-cta">{lang==="fi"?"Avaa portaali":lang==="sv"?"Ã–ppna portal":"Explore portal"} {"\u2192"}</div>
              </div>
            </button>
          </div>
        </div></section>

        {/* FOUNDER */}
        <section className="sec sec-alt" id="founder"><div className="sec-in">
          <div className="fdr"><div className="fdr-img"><div className="fdr-frame"><img src={FOUNDER_IMG} alt="Noah Kraama" className="fdr-photo"/></div>
            {/* v30: Articles under photo â€” clean, no icons, no dates */}
            <div className="art-sec">
              <div className="art-sec-h">{t.art_lab}</div>
              {(lang==="fi"?ARTICLES_FI:lang==="sv"?ARTICLES_SV:ARTICLES_EN).map((a,i)=><button key={i} className="art-link" onClick={()=>setArticle(i)}>
                <span className="art-link-title">{a.title}</span>
              </button>)}
            </div>
          </div>
            <div className="fdr-txt"><div className="sec-lab" style={{textAlign:"left"}}>{t.fdr_lab}</div><h2 className="sec-h2" style={{textAlign:"left",marginBottom:6}}>{t.fdr_name}</h2><div className="fdr-title">{t.fdr_title}</div>
              <div className="fdr-q">{"\u201C"+t.fdr_q+"\u201D"}</div>
              {/* Bio with quotes woven in: para, quote, para, quote, para, quote, para */}
              <p className="fdr-bio">{t.fdr_bio[0]}</p>
              <div className="fdr-pq"><span className="fdr-pq-mark">{"\u201C"}</span><span>{t.fdr_quotes[0]}</span></div>
              <p className="fdr-bio">{t.fdr_bio[1]}</p>
              <div className="fdr-pq"><span className="fdr-pq-mark">{"\u201C"}</span><span>{t.fdr_quotes[1]}</span></div>
              <p className="fdr-bio">{t.fdr_bio[2]}</p>
              <div className="fdr-pq"><span className="fdr-pq-mark">{"\u201C"}</span><span>{t.fdr_quotes[2]}</span></div>
              <p className="fdr-bio">{t.fdr_bio[3]}</p>
              <p className="fdr-bio fdr-personal">{t.fdr_personal}</p></div></div>
          <div className="brd-row"><div className="brd-label">{t.board}</div>
            <div className="brd-cards">{BOARD.map((b,i)=><div key={i} className="brd-c"><div className="brd-av">{b.i}</div><div><div className="brd-n">{b.n}</div><div className="brd-r">{b.r}</div><div className="brd-b">{b.b}</div></div></div>)}</div></div>
        </div></section>

        {/* JURISDICTIONS â€” v17: super clean bank grid */}
        <section className="sec" id="access"><div className="sec-in">
          <div className="sec-lab">{t.acc_lab}</div><h2 className="sec-h2">{t.acc_h}</h2>
          <div className="jur-row">{JURIS.map((j,i)=><div key={i} className="jur">{j.f}<span>{j.n}</span></div>)}</div>
          <div className="acc-section">
            <div className="acc-label">{lang==="fi"?"Suomalaiset pankit":lang==="sv"?"Finska banker":"Finnish Banks"}</div>
            <div className="acc-grid">{BANKS_NORDIC.map((b,i)=><div key={i} className="acc-name">{b.n}</div>)}</div>
            <div className="acc-label">{lang==="fi"?"KansainvÃ¤liset pankit":lang==="sv"?"Internationella banker":"International Banks"}</div>
            <div className="acc-grid lg">{BANKS_INTL.map((b,i)=><div key={i} className="acc-name">{b.n}</div>)}</div>
            <div className="acc-note">{lang==="fi"?"Ja muita. Uusia kumppanuuksia lisÃ¤tÃ¤Ã¤n jatkuvasti.":lang==="sv"?"Och fler. Nya partnerskap lÃ¤ggs till lÃ¶pande.":"And others. New partnerships added continuously."}</div>
          </div>
        </div></section>

        {/* PRICING */}
        <section className="sec sec-alt" id="pricing"><div className="sec-in">
          <div className="sec-lab">{t.price_lab}</div><h2 className="sec-h2">{t.price_h}</h2>
          <p style={{maxWidth:640,margin:"0 auto 36px",color:"var(--t3)",fontSize:15,lineHeight:1.6,textAlign:"center"}}>{t.price_sub}</p>
          <WealthEst t={t} lang={lang}/>
        </div></section>

        {/* v13: FAQ */}
        <section className="sec" id="faq"><div className="sec-in">
          <div className="sec-lab">{t.faq_lab}</div><h2 className="sec-h2">{t.faq_h}</h2>
          <FAQ t={t}/>
        </div></section>

        {/* CTA */}
        <section className="cta"><div className="cta-in"><h2 className="cta-h2">{t.cta_h}</h2><p className="cta-p">{t.cta_p}</p>
          <button className="btn-p btn-lg" onClick={()=>setKyc(true)}><span>{t.cta_btn}</span><Arr/></button></div></section>

        {/* FOOTER */}
        <footer className="ft"><div className="ft-in">
          <div><div className="lg" style={{marginBottom:10}}><Logo size={26}/><div><div className="lg-t">Aureum</div><div className="lg-s">Private Office</div></div></div><p className="ft-desc">{t.ft_desc}</p></div>
          <div className="ft-links">{t.ft_cols.map((col,ci)=><div key={ci} className="ft-col"><span className="ft-ct">{col[0]}</span>{col.slice(1).map((item,ii)=><span key={ii} onClick={ci===0?()=>go(["services","process","pricing"][ii]):ci===1?()=>go(ii===0?"founder":"access"):undefined}>{item}</span>)}</div>)}</div>
        </div><div className="ft-bot"><span>{"\u00A9"} 2026 Aureum Private Office</span><span className="ft-sep">{"\u00B7"}</span><span>aureumprivateoffice.com</span><span className="ft-sep">{"\u00B7"}</span><button className="ft-legal" onClick={()=>setLegal("terms")}>{lang==="fi"?"KÃ¤yttÃ¶ehdot":lang==="sv"?"Villkor":"Terms of Service"}</button><span className="ft-sep">{"\u00B7"}</span><button className="ft-legal" onClick={()=>setLegal("privacy")}>{lang==="fi"?"Tietosuoja":lang==="sv"?"Integritet":"Privacy Policy"}</button></div><div className="ft-disc">{t.ft_disc}</div></footer>
      </div>

      <KYC open={kyc} onClose={()=>setKyc(false)} lang={lang} t={t}/>

      {/* v15: Full-screen modal for report / portal */}
      {fullView&&<div className="fv-overlay" onClick={()=>setFullView(null)}>
        <div className="fv-modal" onClick={e=>e.stopPropagation()}>
          <div className="fv-header">
            <div className="fv-header-left">
              <Logo size={20}/>
              <span className="fv-header-title">{fullView==="report"?(lang==="fi"?"Raportit":lang==="sv"?"Rapporter":"Reports"):(lang==="fi"?"Asiakasportaali":lang==="sv"?"Kundportal":"Client Portal")}</span>
            </div>
            <button className="fv-close" onClick={()=>setFullView(null)}>{"\u2715"}</button>
          </div>
          <div className="fv-body">
            {fullView==="report"?<div className="fv-report-wrap">
              <RPV lang={lang}/>
              <div style={{marginTop:20}}><QReport lang={lang}/></div>
            </div>:
            <Portal lang={lang} t={t}/>}
          </div>
        </div>
      </div>}

      {/* v16: Service detail modal */}
      {svcDetail!==null&&<ServiceDetail svc={svcDetail} onClose={()=>setSvcDetail(null)} lang={lang} onStart={()=>{setSvcDetail(null);setKyc(true)}}/>}

      {/* Legal modal */}
      {legal&&<div className="fv-overlay" onClick={()=>setLegal(null)}>
        <div className="leg-modal" onClick={e=>e.stopPropagation()}>
          <div className="leg-header"><Logo size={18}/><span className="leg-title">Aureum Private Office</span><button className="fv-close" onClick={()=>setLegal(null)}>{"\u2715"}</button></div>
          <div className="leg-body" dangerouslySetInnerHTML={{__html:LEGAL[legal]}}/>
        </div>
      </div>}

      {article!==null&&<div className="fv-overlay" onClick={()=>setArticle(null)}>
        <div className="art-modal" onClick={e=>e.stopPropagation()}>
          <div className="art-header"><button className="fv-close" onClick={()=>setArticle(null)}>{"\u2715"}</button></div>
          <div className="art-body">
            <div className="art-meta"><span className="art-date">{(lang==="fi"?ARTICLES_FI:lang==="sv"?ARTICLES_SV:ARTICLES_EN)[article].date}</span><span className="art-cat">Aureum Private Office</span></div>
            <h1 className="art-h1">{(lang==="fi"?ARTICLES_FI:lang==="sv"?ARTICLES_SV:ARTICLES_EN)[article].title}</h1>
            <p className="art-sub">{(lang==="fi"?ARTICLES_FI:lang==="sv"?ARTICLES_SV:ARTICLES_EN)[article].sub}</p>
            <div className="art-divider"/>
            <div className="art-content" dangerouslySetInnerHTML={{__html:(lang==="fi"?ARTICLES_FI:lang==="sv"?ARTICLES_SV:ARTICLES_EN)[article].body}}/>
            <div className="art-divider"/>
            <div className="art-author"><div className="art-author-av"/><div><div className="art-author-name">Noah Kraama</div><div className="art-author-role">Founder, Aureum Private Office</div></div></div>
          </div>
        </div>
      </div>}

      {/* WhatsApp floating button */}
      <a className="wa-float" href="https://wa.me/message/AUREUM" target="_blank" rel="noopener noreferrer" title={lang==="fi"?"WhatsApp-yhteys":lang==="sv"?"WhatsApp-kontakt":"Contact via WhatsApp"}>
        <svg viewBox="0 0 24 24" width="26" height="26" fill="#fff"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
      </a>

      {/* Cookie consent */}
      {cookie&&<div className="ck-bar">
        <div className="ck-txt">{lang==="fi"?"K\u00E4yt\u00E4mme ev\u00E4steit\u00E4 parantaaksemme kokemustasi. Jatkamalla hyv\u00E4ksyt ev\u00E4steet.":lang==="sv"?"Vi anv\u00E4nder cookies f\u00F6r att f\u00F6rb\u00E4ttra din upplevelse. Genom att forts\u00E4tta accepterar du cookies.":"We use cookies to improve your experience. By continuing, you accept our cookie policy."}</div>
        <div className="ck-acts">
          <button className="ck-acc" onClick={()=>setCookie(false)}>{lang==="fi"?"Hyv\u00E4ksy":lang==="sv"?"Acceptera":"Accept"}</button>
          <button className="ck-dec" onClick={()=>setCookie(false)}>{lang==="fi"?"Hylk\u00E4\u00E4":lang==="sv"?"Avvisa":"Decline"}</button>
        </div>
      </div>}
    </div>
  </>);
}

/* â•â•â• CSS â€” v15: Logo SVG, brand update to Private Office, domain aureumprivateoffice.com â•â•â• */
const CSS = `:root{--navy:#0B1D3A;--navy2:#0E2344;--navy3:#122A4F;--au:#C9A96E;--au-l:#E2CFA5;--au-d:#A68B55;--brd:#1A3258;--brd-l:#1E3A68;--t1:#EEF0F4;--t2:#A0ABBE;--t3:#637896;--t4:#3D5573;}
*{margin:0;padding:0;box-sizing:border-box;}
.au{height:100vh;display:flex;flex-direction:column;background:var(--navy);color:var(--t1);font-family:'Plus Jakarta Sans','Inter',system-ui,sans-serif;font-weight:400;font-size:14px;overflow:hidden;}
.green{color:#3DAA6D!important}.gold{color:var(--au)!important}

/* â•â•â• NAV â€” v13: mobile support â•â•â• */
.nv{position:fixed;top:0;left:0;right:0;z-index:50;padding:16px 40px;transition:all .3s;background:transparent;}
.nv.s{background:rgba(11,29,58,.95);backdrop-filter:blur(20px);border-bottom:1px solid var(--brd);padding:12px 40px;}
.nv-in{max-width:1180px;margin:0 auto;display:flex;align-items:center;justify-content:space-between;}
.nv-r{display:flex;align-items:center;gap:24px;}
.nv-mob{display:none;}
.nv-burger{background:none;border:1px solid var(--brd);color:var(--t2);width:38px;height:38px;display:grid;place-items:center;border-radius:4px;cursor:pointer;transition:all .3s;}.nv-burger:hover{border-color:var(--au);color:var(--au);}
.nv-a{color:var(--t3);font-size:11px;letter-spacing:1px;text-transform:uppercase;cursor:pointer;background:none;border:none;font-family:inherit;transition:color .3s;font-weight:500;}.nv-a:hover{color:var(--t1);}
.nv-cta{padding:9px 22px;background:var(--au);border:none;color:var(--navy);font-family:inherit;font-size:11px;font-weight:600;letter-spacing:1.2px;text-transform:uppercase;cursor:pointer;border-radius:4px;transition:all .3s;}.nv-cta:hover{background:var(--au-l);}
.lang-sw{display:flex;gap:2px;border:1px solid var(--brd);border-radius:4px;padding:2px;}.lang-btn{padding:5px 8px;background:none;border:none;color:var(--t3);font-family:inherit;font-size:10px;font-weight:600;letter-spacing:.5px;cursor:pointer;border-radius:3px;transition:all .2s;}.lang-btn.on{background:var(--au);color:var(--navy);}.lang-btn:hover:not(.on){color:var(--t1);}
.mob-ov{position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:55;backdrop-filter:blur(4px);animation:oIn .3s ease;}
.mob-menu{position:fixed;top:0;right:0;bottom:0;width:280px;background:var(--navy2);z-index:60;transform:translateX(100%);transition:transform .35s cubic-bezier(.4,0,.2,1);display:flex;flex-direction:column;padding:80px 28px 28px;gap:4px;border-left:1px solid var(--brd);}.mob-menu.open{transform:translateX(0);}
.mob-a{text-align:left;padding:14px 0;border:none;border-bottom:1px solid var(--brd);background:none;color:var(--t2);font-family:inherit;font-size:14px;font-weight:500;letter-spacing:.5px;cursor:pointer;transition:color .2s;}.mob-a:hover{color:var(--au);}
.mob-cta{margin-top:16px;padding:14px 24px;background:var(--au);border:none;color:var(--navy);font-family:inherit;font-size:12px;font-weight:700;letter-spacing:1.2px;text-transform:uppercase;cursor:pointer;border-radius:4px;text-align:center;}
.lg{display:flex;align-items:center;gap:10px;}.lg svg{flex-shrink:0;}.lg-t{font-family:'Cormorant Garamond',serif;font-size:18px;font-weight:500;letter-spacing:3px;text-transform:uppercase;}.lg-s{font-size:8px;letter-spacing:2px;text-transform:uppercase;color:var(--t3);margin-top:1px;}
.mn{flex:1;overflow-y:auto;scroll-behavior:smooth;scrollbar-width:thin;scrollbar-color:var(--brd) transparent;}.mn::-webkit-scrollbar{width:4px;}.mn::-webkit-scrollbar-thumb{background:var(--brd);}

/* â•â•â• HERO â€” v13: animated geometric background â•â•â• */
.hero{min-height:100vh;display:flex;align-items:center;position:relative;padding:100px 40px 60px;overflow:hidden;animation:heroIn .8s ease both;}@keyframes heroIn{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
.hero-bg{position:absolute;inset:0;overflow:hidden;}
.hero-grid{position:absolute;inset:0;background-image:linear-gradient(rgba(201,169,110,.03) 1px,transparent 1px),linear-gradient(90deg,rgba(201,169,110,.03) 1px,transparent 1px);background-size:60px 60px;animation:gridShift 20s linear infinite;}
@keyframes gridShift{from{transform:translate(0,0)}to{transform:translate(60px,60px)}}
.hero-glow{position:absolute;border-radius:50%;filter:blur(80px);opacity:.6;animation:glowPulse 8s ease-in-out infinite alternate;}
.hero-glow-1{width:500px;height:500px;top:-100px;left:-50px;background:radial-gradient(circle,rgba(74,143,212,.1) 0%,transparent 70%);}
.hero-glow-2{width:400px;height:400px;bottom:-50px;right:10%;background:radial-gradient(circle,rgba(201,169,110,.08) 0%,transparent 70%);animation-delay:4s;}
@keyframes glowPulse{from{opacity:.4;transform:scale(1)}to{opacity:.7;transform:scale(1.15)}}
.hero-diamond{position:absolute;border:1px solid rgba(201,169,110,.08);transform:rotate(45deg);animation:diamondFloat 12s ease-in-out infinite;}
.hd-0{width:80px;height:80px;top:15%;right:20%;animation-duration:14s;}.hd-1{width:40px;height:40px;top:60%;right:12%;animation-duration:10s;animation-delay:2s;}.hd-2{width:120px;height:120px;top:30%;right:35%;animation-duration:18s;animation-delay:4s;border-color:rgba(74,143,212,.05);}.hd-3{width:30px;height:30px;top:75%;right:30%;animation-duration:11s;animation-delay:1s;}.hd-4{width:60px;height:60px;top:10%;right:45%;animation-duration:16s;animation-delay:3s;border-color:rgba(201,169,110,.06);}.hd-5{width:50px;height:50px;top:50%;right:50%;animation-duration:13s;animation-delay:5s;border-color:rgba(74,143,212,.04);}
@keyframes diamondFloat{0%,100%{transform:rotate(45deg) translate(0,0);opacity:.6}25%{transform:rotate(45deg) translate(8px,-12px);opacity:1}50%{transform:rotate(45deg) translate(-5px,8px);opacity:.4}75%{transform:rotate(45deg) translate(12px,5px);opacity:.8}}
.hero-line{position:absolute;height:1px;background:linear-gradient(90deg,transparent,rgba(201,169,110,.1),transparent);animation:lineSweep 8s ease-in-out infinite;}
.hero-line-1{width:300px;top:25%;right:15%;animation-duration:10s;}.hero-line-2{width:200px;top:55%;right:25%;animation-duration:8s;animation-delay:3s;transform:rotate(-15deg);}.hero-line-3{width:250px;top:70%;right:10%;animation-duration:12s;animation-delay:6s;transform:rotate(8deg);}
@keyframes lineSweep{0%,100%{opacity:0;transform:translateX(-20px)}50%{opacity:1;transform:translateX(20px)}}
.hero-c{max-width:680px;margin-left:max(40px,10vw);position:relative;z-index:2;}
.hero-lab{font-size:11px;letter-spacing:3px;text-transform:uppercase;color:var(--au);margin-bottom:20px;opacity:0;animation:fu .7s ease both .2s;}
.hero-h1{font-family:'Cormorant Garamond',serif;font-size:52px;font-weight:400;line-height:1.2;margin-bottom:24px;opacity:0;animation:fu .7s ease both .35s;}.gld{color:var(--au);}
.hero-p{font-size:15px;color:var(--t2);line-height:1.8;max-width:520px;margin-bottom:24px;opacity:0;animation:fu .7s ease both .5s;}
.hero-fq{max-width:520px;margin-bottom:32px;padding-left:16px;border-left:2px solid var(--au-d);opacity:0;animation:fu .7s ease both .6s;display:flex;flex-direction:column;gap:4px;}
.hero-fq-text{font-family:'Cormorant Garamond',serif;font-size:18px;font-style:italic;color:var(--au-l);line-height:1.5;}
.hero-fq-attr{font-size:11px;color:var(--t3);letter-spacing:.5px;font-weight:500;}
.hero-acts{display:flex;gap:14px;align-items:center;margin-bottom:44px;opacity:0;animation:fu .7s ease both .75s;}
@keyframes fu{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:translateY(0)}}
.btn-p{display:inline-flex;align-items:center;gap:9px;padding:13px 28px;background:var(--au);border:none;color:var(--navy);font-family:inherit;font-size:12px;font-weight:600;letter-spacing:1.2px;text-transform:uppercase;cursor:pointer;border-radius:4px;transition:all .3s;}.btn-p:hover{background:var(--au-l);transform:translateY(-1px);}.btn-lg{padding:16px 36px;font-size:13px;}
.btn-g{color:var(--t3);font-size:12px;letter-spacing:.8px;text-transform:uppercase;padding:13px 24px;border:1px solid var(--brd);background:none;font-family:inherit;cursor:pointer;border-radius:4px;transition:all .3s;}.btn-g:hover{color:var(--t1);border-color:var(--t3);}
.hero-stats{display:grid;grid-template-columns:repeat(4,auto);gap:32px;opacity:0;animation:fu .7s ease both .8s;}
.hero-stat-n{font-family:'Cormorant Garamond',serif;font-size:32px;font-weight:400;color:var(--au);line-height:1;}.hero-stat-l{font-size:11px;color:var(--t3);letter-spacing:.5px;margin-top:3px;}
.sec{padding:80px 40px;opacity:0;transform:translateY(24px);transition:opacity .7s ease,transform .7s ease;}.sec.vis{opacity:1;transform:translateY(0);}.sec-alt{background:var(--navy2);}.sec-in{max-width:1080px;margin:0 auto;}
.sec-lab{font-size:10px;letter-spacing:3px;text-transform:uppercase;color:var(--au);margin-bottom:12px;text-align:center;}
.sec-h2{font-family:'Cormorant Garamond',serif;font-size:36px;font-weight:400;text-align:center;line-height:1.3;margin-bottom:40px;}
.svc4{display:grid;grid-template-columns:repeat(4,1fr);gap:16px;}
.svc{padding:28px 22px;border:1px solid var(--brd);background:var(--navy2);border-radius:6px;transition:all .3s;}.svc:hover{border-color:var(--au-d);transform:translateY(-2px);}
.svc-i{font-size:20px;color:var(--au);margin-bottom:14px;}.svc-t{font-size:16px;font-weight:500;margin-bottom:8px;}.svc-d{font-size:13px;color:var(--t2);line-height:1.65;margin-bottom:14px;}
.svc-tag{font-size:9px;letter-spacing:1.2px;text-transform:uppercase;color:var(--au-d);padding:4px 10px;border:1px solid var(--brd-l);border-radius:3px;display:inline-block;}
.lang-block{display:grid;grid-template-columns:1fr 1fr;gap:40px;align-items:center;}.lang-p{font-size:14px;color:var(--t2);line-height:1.75;margin-bottom:14px;}

.lang-icon{font-size:24px;flex-shrink:0;margin-top:2px;}.lang-ct{font-size:15px;font-weight:500;margin-bottom:3px;}.lang-cd{font-size:12px;color:var(--t3);line-height:1.5;}
.hw-steps{display:grid;grid-template-columns:repeat(4,1fr);gap:16px;}
.hw-step{padding:28px 22px;border:1px solid var(--brd);border-radius:6px;text-align:center;background:var(--navy);}
.hw-n{font-family:'Cormorant Garamond',serif;font-size:28px;color:var(--au);margin-bottom:12px;}.hw-t{font-size:15px;font-weight:500;margin-bottom:8px;}.hw-d{font-size:12px;color:var(--t2);line-height:1.65;margin-bottom:14px;}
.hw-dur{font-size:9px;letter-spacing:1.2px;text-transform:uppercase;color:var(--au-d);padding:4px 10px;border:1px solid var(--brd-l);border-radius:3px;display:inline-block;}

/* â•â•â• v13: SOCIAL PROOF â•â•â• */
.sp{max-width:720px;margin:0 auto;}
.sp-intro{font-size:14px;color:var(--t2);line-height:1.8;margin-bottom:32px;text-align:center;font-style:italic;padding:0 20px;}
.sp-timeline{position:relative;padding-left:48px;margin-bottom:32px;}
.sp-timeline::before{content:'';position:absolute;left:18px;top:8px;bottom:8px;width:1px;background:linear-gradient(to bottom,var(--au-d),var(--brd));}
.sp-step{position:relative;margin-bottom:20px;display:flex;align-items:flex-start;gap:16px;}
.sp-step:last-child{margin-bottom:0;}
.sp-marker{position:absolute;left:-48px;width:36px;height:36px;border:1px solid var(--au-d);border-radius:50%;display:grid;place-items:center;background:var(--navy2);}
.sp-icon{color:var(--au);font-size:14px;}
.sp-day{font-size:10px;letter-spacing:1.5px;text-transform:uppercase;color:var(--au);margin-bottom:3px;font-weight:600;}
.sp-desc{font-size:13px;color:var(--t2);line-height:1.6;}
.sp-results{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:20px;}
.sp-stat{text-align:center;padding:16px 12px;border:1px solid var(--brd);border-radius:6px;background:var(--navy);}
.sp-stat-v{font-family:'Cormorant Garamond',serif;font-size:28px;color:var(--au);line-height:1;margin-bottom:4px;}
.sp-stat-l{font-size:10px;color:var(--t3);letter-spacing:.3px;}
.sp-note{font-size:10px;color:var(--t4);text-align:center;font-style:italic;line-height:1.5;}

.pv-cards{display:grid;grid-template-columns:1fr 1fr;gap:16px;max-width:860px;margin:0 auto;}
.pv-card{display:block;border:1px solid var(--brd);border-radius:8px;background:var(--navy2);cursor:pointer;transition:all .35s;text-align:left;font-family:inherit;color:var(--t1);padding:0;width:100%;}.pv-card:hover{border-color:var(--au-d);transform:translateY(-2px);box-shadow:0 8px 32px rgba(0,0,0,.25);}
.pv-card-inner{padding:28px 24px;}
.pv-card-header{display:flex;align-items:flex-start;gap:14px;margin-bottom:20px;}
.pv-card-icon{width:40px;height:40px;border:1px solid var(--au-d);border-radius:6px;display:grid;place-items:center;color:var(--au);font-size:16px;flex-shrink:0;}
.pv-card-title{font-size:16px;font-weight:500;margin-bottom:2px;}
.pv-card-sub{font-size:11px;color:var(--t3);}
.pv-card-stats{display:flex;gap:0;background:var(--navy);border:1px solid var(--brd);border-radius:6px;overflow:hidden;margin-bottom:18px;}
.pv-card-stat{flex:1;padding:10px 8px;text-align:center;border-right:1px solid var(--brd);}.pv-card-stat:last-child{border-right:none;}
.pv-cs-v{display:block;font-family:'Cormorant Garamond',serif;font-size:18px;font-weight:400;}.pv-cs-l{font-size:8px;letter-spacing:.8px;text-transform:uppercase;color:var(--t3);margin-top:1px;}
.pv-card-features{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:18px;}
.pv-card-feat{padding:6px 12px;border:1px solid var(--brd);border-radius:4px;font-size:11px;color:var(--t2);letter-spacing:.3px;}
.pv-card-cta{font-size:12px;color:var(--au);letter-spacing:.8px;font-weight:500;transition:color .2s;}.pv-card:hover .pv-card-cta{color:var(--au-l);}

/* v15: Full-screen modal */
.fv-overlay{position:fixed;inset:0;background:rgba(0,0,0,.65);z-index:80;backdrop-filter:blur(12px);display:flex;align-items:center;justify-content:center;animation:oIn .3s ease;padding:20px;}
.fv-modal{width:100%;max-width:920px;max-height:90vh;background:var(--navy);border:1px solid var(--brd);border-radius:12px;overflow:hidden;display:flex;flex-direction:column;box-shadow:0 24px 64px rgba(0,0,0,.5);animation:fvIn .35s ease;}
@keyframes fvIn{from{opacity:0;transform:translateY(16px) scale(.97)}to{opacity:1;transform:translateY(0) scale(1)}}
.fv-header{display:flex;align-items:center;justify-content:space-between;padding:14px 20px;border-bottom:1px solid var(--brd);background:var(--navy2);flex-shrink:0;}
.fv-header-left{display:flex;align-items:center;gap:10px;}
.fv-header-title{font-size:14px;font-weight:500;letter-spacing:.5px;}
.fv-close{width:32px;height:32px;border:1px solid var(--brd);background:none;color:var(--t3);font-size:14px;cursor:pointer;display:grid;place-items:center;border-radius:4px;font-family:inherit;transition:all .3s;}.fv-close:hover{color:var(--t1);border-color:var(--t3);}
.fv-body{flex:1;overflow-y:auto;scrollbar-width:thin;scrollbar-color:var(--brd) transparent;padding:20px;}
.fv-report-wrap{max-width:900px;margin:0 auto;overflow:hidden;}
.prev-frame{max-width:860px;margin:0 auto;border:1px solid var(--brd);border-radius:8px;overflow:hidden;background:var(--navy3);}

/* â•â•â• v17: MONTHLY REPORT â•â•â• */
.mr{background:#FFF8F0;color:#1A1A22;font-family:'Plus Jakarta Sans','Inter',sans-serif;border:1px solid #E5DDD0;border-radius:8px;overflow:hidden;}
.mr-mast{display:flex;justify-content:space-between;align-items:center;padding:14px 24px;border-bottom:2px solid #1A1A22;}
.mr-mast-left{display:flex;align-items:center;gap:12px;}.mr-mast-right{display:flex;align-items:center;gap:12px;}
.mr-mast-tag{font-size:9px;letter-spacing:1.5px;text-transform:uppercase;color:#fff;background:#1A1A22;padding:4px 10px;font-weight:600;}
.mr-mast-date{font-size:12px;color:#666;}.mr-mast-acct{font-size:12px;color:#444;font-weight:500;}.mr-mast-id{font-size:11px;color:#999;}
.mr-hero{display:flex;justify-content:space-between;align-items:flex-end;padding:24px;border-bottom:1px solid #E5DDD0;}
.mr-hero-main{}.mr-hero-label{font-size:9px;letter-spacing:1.5px;text-transform:uppercase;color:#999;margin-bottom:4px;}.mr-hero-val{font-family:'Cormorant Garamond',serif;font-size:36px;font-weight:400;line-height:1;}
.mr-hero-kpis{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;}
.mr-kpi{text-align:center;display:flex;flex-direction:column;justify-content:center;align-items:center;min-height:50px;}.mr-kv{font-family:'Cormorant Garamond',serif;font-size:18px;font-weight:400;line-height:1.2;}.mr-kl{font-size:8px;letter-spacing:.8px;text-transform:uppercase;color:#999;margin-top:2px;}
.mr-section{padding:16px 24px;border-bottom:1px solid #E5DDD0;}
.mr-sh{font-family:'Cormorant Garamond',serif;font-size:15px;font-weight:500;margin-bottom:10px;color:#1A1A22;}.mr-sh-icon{display:flex;align-items:center;gap:6px;}
.mr-chart-leg{display:flex;gap:16px;margin-bottom:6px;}.mr-leg{display:flex;align-items:center;gap:4px;font-size:10px;color:#999;}
.mr-two-col{display:grid;grid-template-columns:1fr 1fr;gap:20px;padding:16px 24px;border-bottom:1px solid #E5DDD0;}
.mr-col{}
.mr-alloc-list{display:flex;flex-direction:column;gap:4px;}.mr-alloc-item{display:flex;align-items:center;gap:6px;font-size:11px;color:#666;}.mr-alloc-name{flex:1;}.mr-alloc-pct{font-weight:600;color:#333;min-width:30px;text-align:right;}
.mr-ccy-list{display:flex;flex-direction:column;gap:6px;}.mr-ccy-item{display:flex;align-items:center;gap:8px;font-size:11px;}
.mr-ccy-bar-wrap{flex:1;height:8px;background:#F0EDE8;border-radius:4px;overflow:hidden;}.mr-ccy-bar{height:100%;border-radius:4px;transition:width .5s;}
.mr-ccy-code{font-weight:600;color:#333;min-width:30px;}.mr-ccy-pct{color:#666;min-width:24px;text-align:right;}
.mr-tbl{font-size:11px;border:1px solid #E5DDD0;border-radius:6px;overflow:hidden;}
.mr-tbl-hdr{display:flex;padding:8px 12px;background:#F5F2ED;font-weight:600;color:#666;border-bottom:1px solid #E5DDD0;}
.mr-th{flex:1;font-size:9px;letter-spacing:.5px;text-transform:uppercase;}.mr-th.r{text-align:right;}
.mr-tbl-row{display:flex;padding:7px 12px;border-bottom:1px solid #F2F0EC;align-items:center;}.mr-tbl-row.alt{background:#FDFCF9;}.mr-tbl-row:last-child{border-bottom:none;}
.mr-td{flex:1;font-size:11px;color:#333;}.mr-td.r{text-align:right;}.mr-td-sec{color:#999;font-size:10px;}
.mr-td.red{color:#C0392B;}.mr-td.grn{color:#27AE60;}
.mr-wl-row{display:flex;align-items:center;gap:8px;padding:6px 0;border-bottom:1px solid #F2F0EC;font-size:12px;}.mr-wl-row:last-child{border-bottom:none;}
.mr-wl-n{flex:1;font-weight:500;color:#333;}.mr-wl-r{font-weight:600;min-width:48px;text-align:right;}.mr-wl-r.grn{color:#27AE60;}.mr-wl-r.red{color:#C0392B;}.mr-wl-c{color:#999;font-size:10px;min-width:44px;text-align:right;}
.mr-fees{}.mr-fee-line-compact{display:flex;flex-wrap:wrap;align-items:center;gap:4px 6px;font-size:11px;color:#666;padding:10px 14px;background:#FAFAF8;border:1px solid #E5DDD0;border-radius:6px;margin-bottom:6px;}.mr-fee-line-compact strong{color:#1A1A22;font-size:12px;}.mr-fee-sep{color:#CCC;}.mr-fee-au{color:#8B7340;font-weight:600;}
.mr-fee-selling{font-size:11px;color:#3DAA6D;font-weight:500;letter-spacing:.3px;text-align:center;padding:6px 0;}
.qr-fee-compact{border:1px solid #E5DDD0;border-radius:8px;overflow:hidden;margin-bottom:10px;}.qr-fee-main{display:flex;align-items:baseline;gap:10px;padding:12px 14px;background:#FAFAF8;}.qr-fee-main span:first-child{font-size:12px;color:#666;}.qr-fee-big{font-family:'Cormorant Garamond',serif;font-size:24px;font-weight:600;color:#1A1A22;}.qr-fee-vs{font-size:11px;color:#999;}.qr-fee-line-items{font-size:11px;color:#666;padding:8px 14px;border-top:1px solid #E5DDD0;}

.mr-disc{padding:12px 24px;font-size:9px;color:#bbb;text-align:center;font-style:italic;line-height:1.4;}

/* shared dot/bar */
.rp-dot{width:6px;height:6px;border-radius:50%;flex-shrink:0;}
.rp-stack-bar{display:flex;height:10px;border-radius:5px;overflow:hidden;gap:1px;margin-bottom:6px;}
.rp-stack-seg{height:100%;transition:width .6s ease;}
.rp-stack-labels{display:flex;flex-wrap:wrap;gap:3px 8px;}
.rp-stack-lbl{display:inline-flex;align-items:center;gap:3px;font-size:9px;color:#888;}
.wa{font-family:'Plus Jakarta Sans','Inter',sans-serif;overflow:hidden;}.wa-h{background:#075E54;padding:14px 18px;display:flex;align-items:center;gap:12px;}.wa-ava{width:36px;height:36px;background:var(--au);color:#fff;font-size:14px;font-weight:600;display:grid;place-items:center;border-radius:50%;}.wa-name{font-size:14px;font-weight:500;color:#fff;}.wa-st{font-size:11px;color:rgba(255,255,255,.65);}
.wa-body{background:#E4DDD6;padding:16px;max-height:420px;overflow-y:auto;}.wa-m{margin-bottom:10px;display:flex;}.wa-m.u{justify-content:flex-end;}.wa-m.b{justify-content:flex-start;}
.wa-b{max-width:82%;padding:10px 14px;border-radius:8px;font-size:13px;line-height:1.7;color:#111;box-shadow:0 1px 2px rgba(0,0,0,.08);}.wa-b.u{background:#D9FDD3;border-bottom-right-radius:2px;}.wa-b.b{background:#fff;border-bottom-left-radius:2px;}.wa-tm{font-size:10px;color:#999;text-align:right;margin-top:4px;}
.fdr{display:grid;grid-template-columns:280px 1fr;gap:48px;align-items:start;margin-bottom:56px;}.fdr-frame{width:100%;aspect-ratio:3/4;border:1px solid var(--brd);background:var(--navy);display:flex;align-items:center;justify-content:center;border-radius:6px;}.fdr-photo{width:100%;height:100%;object-fit:cover;border-radius:6px;filter:brightness(.95) contrast(1.05);}
.fdr-title{font-size:12px;color:var(--au);letter-spacing:1.5px;text-transform:uppercase;margin-bottom:18px;}.fdr-q{font-family:'Cormorant Garamond',serif;font-size:19px;font-style:italic;line-height:1.7;margin-bottom:20px;padding-left:18px;border-left:2px solid var(--au-d);}
.fdr-bio{font-size:13.5px;color:var(--t2);line-height:1.8;margin-bottom:10px;}.fdr-personal{color:var(--t3);font-size:13px;}
.fdr-pq{margin:20px 0;padding:14px 0 14px 18px;border-left:2px solid var(--au-d);font-family:'Cormorant Garamond',serif;font-size:17px;font-weight:400;color:var(--au-l);line-height:1.55;font-style:italic;}
.fdr-pq-mark{color:var(--au);font-size:24px;font-style:normal;margin-right:3px;line-height:1;vertical-align:-3px;}

/* v30: Articles under founder photo â€” minimal */
.art-sec{margin-top:24px;}
.art-sec-h{font-size:10px;letter-spacing:2px;text-transform:uppercase;color:var(--au-d);margin-bottom:12px;font-weight:400;}
.art-link{display:block;width:100%;padding:10px 0;border:none;border-bottom:1px solid var(--brd);background:none;cursor:pointer;text-align:left;font-family:inherit;transition:all .2s;color:var(--t2);}.art-link:first-of-type{border-top:1px solid var(--brd);}
.art-link:hover{color:var(--au-l);padding-left:6px;}
.art-link-title{font-size:12px;line-height:1.5;}

/* Article reading modal */
.art-modal{max-width:680px;max-height:90vh;background:var(--navy);border:1px solid var(--brd);border-radius:10px;margin:auto;display:flex;flex-direction:column;overflow:hidden;}
.art-header{display:flex;justify-content:flex-end;padding:16px 20px 0;}
.art-body{flex:1;overflow-y:auto;padding:8px 48px 48px;-webkit-overflow-scrolling:touch;}
.art-meta{display:flex;gap:16px;align-items:center;margin-bottom:20px;}.art-date,.art-cat{font-size:11px;color:var(--t3);letter-spacing:.5px;text-transform:uppercase;}
.art-h1{font-family:'Cormorant Garamond',serif;font-size:32px;font-weight:400;line-height:1.25;margin-bottom:12px;color:var(--t1);}
.art-sub{font-size:14px;color:var(--t3);line-height:1.6;font-style:italic;margin-bottom:24px;}
.art-divider{height:1px;background:var(--brd);margin:8px 0 28px;}
.art-content p{font-size:14px;color:var(--t2);line-height:1.85;margin-bottom:16px;}
.art-content blockquote{margin:28px 0;padding:16px 0 16px 20px;border-left:2px solid var(--au-d);font-family:'Cormorant Garamond',serif;font-size:19px;font-style:italic;color:var(--au-l);line-height:1.5;}
.art-content .art-sign{margin-top:32px;font-size:13px;color:var(--t3);line-height:1.7;font-style:italic;}
.art-author{display:flex;align-items:center;gap:14px;margin-top:8px;}
.art-author-av{width:40px;height:40px;border-radius:50%;background:linear-gradient(135deg,var(--au-d),var(--au));flex-shrink:0;}
.art-author-name{font-size:14px;font-weight:600;color:var(--t1);}.art-author-role{font-size:12px;color:var(--t3);}
.brd-row{border-top:1px solid var(--brd);padding-top:40px;}.brd-label{font-size:10px;letter-spacing:3px;text-transform:uppercase;color:var(--au);margin-bottom:20px;}
.brd-cards{display:grid;grid-template-columns:repeat(2,1fr);gap:16px;}.brd-c{display:flex;gap:14px;padding:20px;border:1px solid var(--brd);border-radius:6px;background:var(--navy);transition:border-color .3s;}.brd-c:hover{border-color:var(--au-d);}
.brd-av{width:40px;height:40px;border:1px solid var(--au-d);display:grid;place-items:center;font-family:'Cormorant Garamond',serif;font-size:16px;color:var(--au);flex-shrink:0;border-radius:4px;}
.brd-n{font-size:14px;font-weight:500;margin-bottom:1px;}.brd-r{font-size:11px;color:var(--au-d);letter-spacing:.5px;text-transform:uppercase;margin-bottom:4px;}.brd-b{font-size:12px;color:var(--t3);line-height:1.5;}
.jur-row{display:flex;flex-wrap:wrap;justify-content:center;gap:12px;margin-bottom:24px;}.jur{display:flex;align-items:center;gap:6px;padding:10px 16px;border:1px solid var(--brd);border-radius:6px;font-size:13px;background:var(--navy2);}.jur span{letter-spacing:.3px;}
.bnk-row{display:flex;flex-wrap:wrap;justify-content:center;gap:8px;}.bnk{font-size:12px;color:var(--t3);padding:6px 14px;border:1px solid var(--brd);border-radius:4px;letter-spacing:.5px;}
.calc{border:1px solid var(--brd);border-radius:8px;padding:24px;background:var(--navy2);}
.we-presets{display:flex;align-items:center;gap:6px;margin-bottom:20px;}.we-pre{padding:7px 16px;border:1px solid var(--brd);background:none;color:var(--t3);font-family:inherit;font-size:11px;cursor:pointer;border-radius:4px;transition:all .2s;letter-spacing:.3px;}.we-pre.on{background:var(--au);color:var(--navy);border-color:var(--au);}.we-pre:hover:not(.on){border-color:var(--t3);color:var(--t1);}
.we-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px 24px;margin-bottom:20px;}
.we-sl{}.we-sl-top{display:flex;justify-content:space-between;align-items:baseline;margin-bottom:6px;}.we-sl-l{font-size:11px;color:var(--t3);letter-spacing:.3px;}.we-sl-v{font-family:'Cormorant Garamond',serif;font-size:22px;color:var(--au);}
.we-sl-mm{display:flex;justify-content:space-between;font-size:9px;color:var(--t4);margin-top:2px;}
.we-bands{display:flex;flex-wrap:wrap;gap:4px;margin-top:8px;}
.we-band{padding:7px 12px;border:1px solid var(--brd);background:none;color:var(--t3);font-family:inherit;font-size:11px;cursor:pointer;border-radius:4px;transition:all .2s;letter-spacing:.3px;font-weight:500;}.we-band.on{background:var(--au);color:var(--navy);border-color:var(--au);}.we-band:hover:not(.on){border-color:var(--t3);color:var(--t1);}
.we-fee-compare{display:flex;align-items:center;gap:12px;padding:18px 0;margin-top:8px;border-top:1px solid var(--brd);}
.we-fee-box{flex:1;padding:14px 16px;border:1px solid var(--brd);border-radius:8px;text-align:center;background:var(--navy);transition:all .3s;}
.we-fee-box.aur{border-color:var(--au-d);background:rgba(201,169,110,.04);}
.we-fee-label{font-size:9px;letter-spacing:1.2px;text-transform:uppercase;color:var(--t4);margin-bottom:4px;}
.we-fee-val{font-family:'Cormorant Garamond',serif;font-size:28px;font-weight:400;line-height:1.1;}
.we-fee-box.typ .we-fee-val{color:#637896;}.we-fee-box.aur .we-fee-val{color:var(--au);}
.we-fee-abs{font-size:11px;color:var(--t3);margin-top:4px;}
.we-fee-arrow{color:var(--t4);font-size:18px;flex-shrink:0;}
.we-fee-save{text-align:center;flex-shrink:0;padding:0 8px;}
.we-fee-save-val{font-family:'Cormorant Garamond',serif;font-size:24px;color:#3DAA6D;font-weight:500;line-height:1;}
.we-fee-save-lbl{font-size:9px;letter-spacing:1px;text-transform:uppercase;color:#3DAA6D;margin-top:2px;}
.we-layers{margin-top:10px;padding-top:8px;border-top:1px solid var(--brd);display:flex;flex-direction:column;gap:5px;}
.we-layer{display:flex;align-items:center;gap:6px;font-size:10px;position:relative;}
.we-layer-bar{height:4px;background:linear-gradient(90deg,#8B4A4A,#C06060);border-radius:2px;flex-shrink:0;min-width:8px;transition:width .4s ease;}
.we-layer-name{flex:1;color:var(--t3);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.we-layer-val{color:var(--t2);font-weight:500;font-variant-numeric:tabular-nums;flex-shrink:0;}
.we-aur-note{font-size:9px;color:var(--au-d);margin-top:6px;letter-spacing:.2px;font-style:italic;}
.calc-rng{width:100%;height:3px;-webkit-appearance:none;background:var(--brd);border-radius:2px;outline:none;margin:6px 0 2px;}.calc-rng::-webkit-slider-thumb{-webkit-appearance:none;width:16px;height:16px;background:var(--t2);border-radius:50%;cursor:pointer;border:2px solid var(--navy2);transition:all .2s;}.calc-rng::-webkit-slider-thumb:hover{transform:scale(1.15);}
.calc-rng.rng-gold::-webkit-slider-thumb{background:var(--au);}
.calc-rng.rng-dim::-webkit-slider-thumb{background:#637896;}
.we-chart{margin-bottom:16px;}.we-legend{display:flex;gap:16px;margin-bottom:8px;}.we-leg{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--t3);}
.we-results{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:14px;}.we-r{padding:14px 12px;border:1px solid var(--brd);border-radius:6px;text-align:center;}.we-r.hi{border-color:var(--au-d);background:rgba(201,169,110,.05);}.we-rl{font-size:10px;color:var(--t3);margin-bottom:3px;letter-spacing:.3px;}.we-rv{font-family:'Cormorant Garamond',serif;font-size:22px;}.we-rs{font-size:10px;color:var(--t4);margin-top:2px;}
.calc-fn{font-size:10px;color:var(--t4);line-height:1.5;font-style:italic;text-align:center;}

/* â•â•â• v13: FAQ ACCORDION â•â•â• */
.faq-list{max-width:720px;margin:0 auto;}
.faq-item{border-bottom:1px solid var(--brd);overflow:hidden;}
.faq-q{display:flex;justify-content:space-between;align-items:center;width:100%;padding:18px 0;background:none;border:none;color:var(--t1);font-family:inherit;font-size:15px;font-weight:500;cursor:pointer;text-align:left;transition:color .3s;gap:16px;line-height:1.4;}
.faq-q:hover{color:var(--au);}
.faq-item.open .faq-q{color:var(--au);}
.faq-icon{font-size:20px;color:var(--au);flex-shrink:0;width:24px;text-align:center;font-weight:300;}
.faq-a{max-height:0;overflow:hidden;transition:max-height .4s cubic-bezier(.4,0,.2,1);}
.faq-item.open .faq-a{max-height:500px;}
.faq-a-in{padding:0 0 18px;font-size:13.5px;color:var(--t2);line-height:1.75;}

.cta{padding:80px 40px;text-align:center;background:radial-gradient(ellipse at center,rgba(201,169,110,.05) 0%,transparent 60%);opacity:0;transform:translateY(24px);transition:opacity .7s ease,transform .7s ease;}.cta.vis{opacity:1;transform:translateY(0);}.cta-in{max-width:520px;margin:0 auto;}.cta-h2{font-family:'Cormorant Garamond',serif;font-size:34px;font-weight:400;margin-bottom:14px;}.cta-p{font-size:14px;color:var(--t2);line-height:1.7;margin-bottom:28px;}
.ft{border-top:1px solid var(--brd);padding:40px 40px 0;background:var(--navy2);}.ft-in{max-width:1080px;margin:0 auto;display:grid;grid-template-columns:1fr 2fr;gap:40px;margin-bottom:32px;}.ft-desc{font-size:13px;color:var(--t3);line-height:1.6;margin-top:4px;}
.ft-links{display:grid;grid-template-columns:repeat(3,1fr);gap:16px;}.ft-col{display:flex;flex-direction:column;gap:6px;}.ft-ct{font-size:9px;letter-spacing:2px;text-transform:uppercase;color:var(--t4);margin-bottom:2px;font-weight:600;}.ft-col span{color:var(--t3);font-size:13px;cursor:pointer;transition:color .2s;}.ft-col span:hover{color:var(--t1);}
.ft-bot{border-top:1px solid var(--brd);padding:16px 0;text-align:center;font-size:11px;color:var(--t4);max-width:1080px;margin:0 auto;display:flex;flex-wrap:wrap;justify-content:center;align-items:center;gap:4px;}.ft-sep{color:var(--t4);opacity:.5;}.ft-legal{background:none;border:none;color:var(--t3);font-size:11px;cursor:pointer;text-decoration:underline;text-underline-offset:2px;transition:color .2s;padding:0;}.ft-legal:hover{color:var(--au);}
.ft-disc{text-align:center;font-size:10px;color:var(--t4);max-width:1080px;margin:8px auto 0;padding:0 20px;line-height:1.5;opacity:.7;}
.portal{background:#FAFAF7;color:#1A1A22;font-family:'Plus Jakarta Sans','Inter',sans-serif;border-radius:8px;overflow:hidden;border:1px solid #E2E0DB;max-width:860px;margin:0 auto;}
.portal-hd{display:flex;justify-content:space-between;align-items:center;padding:20px 24px;border-bottom:1px solid #E8E5E0;background:#fff;}.portal-user{display:flex;align-items:center;gap:12px;}.portal-av{width:40px;height:40px;background:#0B1D3A;color:#C9A96E;font-size:14px;font-weight:600;display:grid;place-items:center;border-radius:8px;}.portal-nm{font-size:15px;font-weight:600;}.portal-id{font-size:11px;color:#999;margin-top:1px;}
.portal-meta{display:flex;gap:20px;}.portal-meta div{display:flex;flex-direction:column;align-items:flex-end;}.portal-ml{font-size:9px;letter-spacing:1px;text-transform:uppercase;color:#bbb;}.portal-mv{font-size:12px;font-weight:500;margin-top:1px;}
.portal-tabs{display:flex;background:#F2F0EC;padding:3px;}.portal-tab{flex:1;padding:10px;text-align:center;font-size:12px;font-weight:500;border:none;background:none;cursor:pointer;color:#888;transition:all .2s;font-family:inherit;}.portal-tab.on{background:#fff;color:#1A1A22;box-shadow:0 1px 4px rgba(0,0,0,.06);}
.portal-body{min-height:280px;padding:20px 24px;}
.portal-kpis{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:16px;}.portal-kpi{background:#fff;border:1px solid #E8E5E0;border-radius:8px;padding:12px;text-align:center;display:flex;flex-direction:column;justify-content:center;align-items:center;min-height:70px;}.portal-kv{font-family:'Cormorant Garamond',serif;font-size:20px;font-weight:400;line-height:1.2;}.portal-kv.green{color:#2D8A5E;}.portal-kv.gold{color:#A68B55;}.portal-kl{font-size:9px;letter-spacing:.8px;text-transform:uppercase;color:#999;margin-top:3px;}
.portal-chart{background:#fff;border:1px solid #E8E5E0;border-radius:8px;padding:12px;margin-bottom:14px;}
.portal-act-t{font-size:13px;font-weight:600;margin-bottom:8px;}.portal-ar{display:flex;align-items:center;gap:12px;padding:7px 0;border-bottom:1px solid #F2F0EC;font-size:13px;}.portal-ad{color:#999;min-width:50px;font-size:11px;}.portal-at{flex:1;}.portal-as{font-size:10px;letter-spacing:.5px;text-transform:uppercase;padding:3px 8px;border-radius:3px;font-weight:500;}
.portal-as.report{background:rgba(74,143,212,.1);color:#4A8FD4;}.portal-as.insight{background:rgba(45,138,94,.1);color:#2D8A5E;}.portal-as.fee{background:rgba(201,169,110,.1);color:#A68B55;}.portal-as.bench{background:rgba(155,124,196,.1);color:#7B6BA5;}
.portal-ph{font-size:14px;font-weight:600;margin-bottom:12px;}.portal-pr{display:grid;grid-template-columns:1fr 70px 80px;gap:10px;align-items:center;padding:10px 0;border-bottom:1px solid #F2F0EC;font-size:13px;}
.portal-ps{font-size:10px;letter-spacing:.5px;text-transform:uppercase;padding:3px 8px;border-radius:3px;font-weight:500;text-align:center;}.portal-ps.selected{background:rgba(201,169,110,.15);color:#A68B55;}.portal-ps.reviewed{background:rgba(74,143,212,.1);color:#4A8FD4;}.portal-ps.meeting{background:rgba(45,138,94,.1);color:#2D8A5E;}.portal-ps.pending{background:#F2F0EC;color:#999;}
.portal-rr{display:flex;align-items:center;gap:12px;padding:10px 0;border-bottom:1px solid #F2F0EC;font-size:13px;}.portal-mr{display:flex;align-items:center;gap:12px;padding:10px 0;border-bottom:1px solid #F2F0EC;font-size:13px;}
.portal-ft{text-align:center;padding:12px;font-size:11px;color:#bbb;background:#F2F0EC;font-style:italic;}
.ov{position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:90;backdrop-filter:blur(8px);animation:oIn .3s ease;}@keyframes oIn{from{opacity:0}to{opacity:1}}
.ky-overlay{position:fixed;inset:0;background:rgba(0,0,0,.6);z-index:99;backdrop-filter:blur(4px);}
.ky{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%) scale(.95);width:min(520px,94vw);height:min(680px,90vh);background:var(--navy);z-index:100;opacity:0;pointer-events:none;transition:all .35s cubic-bezier(.4,0,.2,1);display:flex;flex-direction:column;border:1px solid var(--brd);border-radius:12px;box-shadow:0 24px 64px rgba(0,0,0,.5);overflow:hidden;}.ky.open{opacity:1;pointer-events:auto;transform:translate(-50%,-50%) scale(1);}
.ky-h{display:flex;align-items:center;justify-content:space-between;padding:14px 18px;border-bottom:1px solid var(--brd);background:var(--navy2);flex-shrink:0;}
.ky-hl{display:flex;align-items:center;gap:10px;}.ky-dia{width:18px;height:18px;border:1px solid var(--au);transform:rotate(45deg);position:relative;}.ky-dia::after{content:'';position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);width:4px;height:4px;background:var(--au);}
.ky-ht{font-size:13px;font-weight:500;}.ky-hp{font-size:10px;color:var(--au-d);letter-spacing:1px;text-transform:uppercase;margin-top:1px;}
.ky-hr{display:flex;align-items:center;gap:8px;}.ky-bb{padding:5px 10px;border:1px solid var(--brd);background:none;color:var(--t3);font-family:inherit;font-size:10px;letter-spacing:1px;text-transform:uppercase;cursor:pointer;border-radius:3px;transition:all .3s;}.ky-bb:hover,.ky-bb.on{border-color:var(--au-d);color:var(--au);}
.ky-x{width:30px;height:30px;border:1px solid var(--brd);background:none;color:var(--t3);font-size:13px;cursor:pointer;display:grid;place-items:center;border-radius:3px;font-family:inherit;transition:all .3s;}.ky-x:hover{color:var(--t1);border-color:var(--t3);}
.ky-prog{height:2px;background:var(--brd);flex-shrink:0;}.ky-prog-f{height:100%;background:linear-gradient(90deg,var(--au-d),var(--au));transition:width .7s ease;}
.ky-body{flex:1;overflow-y:auto;scrollbar-width:thin;scrollbar-color:var(--brd) transparent;}
.ky-bf{padding:18px;}.ky-bs{margin-bottom:12px;}.ky-bst{font-size:9px;letter-spacing:2px;text-transform:uppercase;color:var(--au-d);margin-bottom:6px;font-weight:600;}
.ky-br{display:flex;justify-content:space-between;padding:5px 0;border-bottom:1px solid var(--brd);}.ky-bk{font-size:11px;color:var(--t3);}.ky-bv{font-size:11px;color:var(--t1);}.ky-be{font-size:10px;color:var(--t4);font-style:italic;}
.ky-chat{padding:18px;}.ky-m{margin-bottom:14px;animation:kI .3s ease forwards;opacity:0;}@keyframes kI{from{opacity:0;transform:translateY(5px)}to{opacity:1;transform:translateY(0)}}
.ky-ma{display:flex;gap:10px;align-items:flex-start;}.ky-av{width:26px;height:26px;border:1px solid var(--au-d);border-radius:4px;position:relative;flex-shrink:0;margin-top:2px;}.ky-av::after{content:'';position:absolute;top:50%;left:50%;transform:translate(-50%,-50%) rotate(45deg);width:6px;height:6px;background:var(--au);}
.ky-ba{background:var(--navy2);border:1px solid var(--brd);border-radius:6px;padding:12px 14px;font-size:13px;line-height:1.7;max-width:370px;white-space:pre-wrap;}
.ky-mu{display:flex;justify-content:flex-end;padding-left:36px;}.ky-bu{background:rgba(201,169,110,.08);border:1px solid rgba(201,169,110,.18);border-radius:6px;padding:10px 14px;font-size:13px;line-height:1.6;max-width:320px;color:var(--au-l);}
.ky-qr{display:flex;flex-wrap:wrap;gap:5px;margin-top:8px;margin-left:36px;}
.ky-qr-wrap{display:flex;flex-wrap:wrap;gap:6px;padding:0 4px;}
.ky-qrb{padding:8px 14px;border:1px solid var(--brd);background:var(--navy);color:var(--t2);font-family:inherit;font-size:12px;cursor:pointer;border-radius:6px;transition:all .2s;text-align:left;line-height:1.4;}.ky-qrb:hover{border-color:var(--au);color:var(--au-l);}.ky-qrb.on{border-color:var(--au);background:rgba(201,169,110,.12);color:var(--au-l);}
.ky-confirm{width:100%;padding:10px;margin-top:8px;border:none;background:var(--au);color:var(--navy);font-family:inherit;font-size:13px;font-weight:600;cursor:pointer;border-radius:6px;transition:all .2s;letter-spacing:.3px;}.ky-confirm:hover{background:var(--au-l);}
.ky-done{text-align:center;padding:8px;}
.ky-ty{display:flex;gap:4px;background:var(--navy2);border:1px solid var(--brd);border-radius:6px;padding:14px 16px;}.ky-ty span{width:5px;height:5px;background:var(--au-d);border-radius:50%;animation:tp 1.4s ease infinite;}.ky-ty span:nth-child(2){animation-delay:.2s}.ky-ty span:nth-child(3){animation-delay:.4s}@keyframes tp{0%,60%,100%{opacity:.2}30%{opacity:1}}
.ky-ia{padding:12px 18px 16px;border-top:1px solid var(--brd);background:var(--navy2);flex-shrink:0;}.ky-ir{display:flex;gap:8px;}
.ky-ii{flex:1;background:var(--navy);border:1px solid var(--brd);color:var(--t1);padding:10px 14px;font-family:inherit;font-size:13px;outline:none;resize:none;min-height:40px;max-height:100px;border-radius:6px;transition:border-color .3s;line-height:1.5;}.ky-ii:focus{border-color:var(--au-d);}.ky-ii::placeholder{color:var(--t4);}
.ky-se{width:40px;height:40px;background:var(--au);border:none;color:var(--navy);font-size:15px;cursor:pointer;border-radius:4px;display:grid;place-items:center;flex-shrink:0;transition:all .3s;}.ky-se:hover{background:var(--au-l);}.ky-se:disabled{opacity:.2;cursor:not-allowed;}
.ky-sn{display:flex;align-items:center;gap:6px;justify-content:center;margin-top:8px;font-size:10px;color:var(--t4);}

/* â•â•â• v16: SERVICE CARDS â€” clickable â•â•â• */
.svc-link{cursor:pointer;text-align:left;font-family:inherit;color:inherit;width:100%;display:flex;flex-direction:column;}
.svc-bot{display:flex;justify-content:space-between;align-items:center;margin-top:auto;padding-top:12px;}
.svc-more{font-size:11px;color:var(--au);letter-spacing:.5px;opacity:0;transition:all .3s;}.svc:hover .svc-more{opacity:1;}

/* â•â•â• v16: LANGUAGE â€” flag-focused â•â•â• */
.lang-hero-p{max-width:600px;margin:0 auto 40px;color:var(--t3);font-size:15px;line-height:1.7;text-align:center;}
.lang-hero-p2{max-width:500px;margin:32px auto 0;color:var(--t4);font-size:13px;line-height:1.6;text-align:center;font-style:italic;}
.lang-cards{display:flex;flex-direction:column;gap:0;max-width:620px;margin:0 auto;}
.lang-card{position:relative;display:flex;align-items:center;gap:20px;padding:24px 28px;border-bottom:1px solid var(--brd);cursor:default;transition:all .35s;}
.lang-card:last-child{border-bottom:none;}
.lang-card:hover{background:rgba(201,169,110,.04);padding-left:36px;}
.lang-card-icon{font-size:32px;line-height:1;flex-shrink:0;}
.lang-card-body{flex:1;}
.lang-card-name{font-family:'Cormorant Garamond',serif;font-size:22px;font-weight:500;color:var(--au);margin-bottom:4px;}
.lang-card-desc{font-size:12px;color:var(--t3);line-height:1.5;}
.lang-tip{position:absolute;left:50%;bottom:calc(100% + 10px);transform:translateX(-50%) translateY(6px);opacity:0;pointer-events:none;transition:all .3s ease;background:#0E2344;border:1px solid var(--au-d);border-radius:8px;padding:16px 20px;width:300px;box-shadow:0 10px 30px rgba(0,0,0,.6);z-index:10;}
.lang-card:hover .lang-tip{opacity:1;transform:translateX(-50%) translateY(0);}
.lang-tip::after{content:'';position:absolute;top:100%;left:50%;transform:translateX(-50%);border:7px solid transparent;border-top-color:#0E2344;}
.lang-tip-quote{font-size:12px;color:#E8E4DF;line-height:1.6;font-style:italic;margin-bottom:6px;}
.lang-tip-attr{font-size:10px;color:var(--au);font-weight:500;letter-spacing:.3px;}

/* â•â•â• v17: ACCESS â€” clean name grid â•â•â• */
.acc-section{max-width:900px;margin:32px auto 0;}
.acc-label{font-size:10px;letter-spacing:2px;text-transform:uppercase;color:var(--au);margin:28px 0 12px;font-weight:600;padding-bottom:8px;border-bottom:1px solid var(--brd);}
.acc-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:0;}
.acc-grid.lg{grid-template-columns:repeat(auto-fill,minmax(180px,1fr));}
.acc-name{padding:10px 0;font-size:13px;color:var(--t2);font-weight:400;border-bottom:1px solid rgba(26,50,88,.3);letter-spacing:.2px;transition:color .2s;}.acc-name:hover{color:var(--au);}
.acc-note{text-align:center;font-size:11px;color:var(--t4);margin-top:20px;font-style:italic;}

/* â•â•â• v16: SERVICE DETAIL MODAL â•â•â• */
.sd-modal{max-width:960px;}
.sd-body{padding:0 32px 32px;}
.sd-test{padding:32px;border-bottom:1px solid var(--brd);margin:-20px -32px 28px;background:rgba(201,169,110,.03);}
.sd-test-q{font-family:'Cormorant Garamond',serif;font-size:20px;font-style:italic;line-height:1.7;color:var(--au-l);margin-bottom:10px;}
.sd-test-who{font-size:12px;color:var(--t3);letter-spacing:.5px;}
.sd-content{}
.sd-intro{font-size:14px;color:var(--t2);line-height:1.8;margin-bottom:28px;}
.sd-sh{font-family:'Cormorant Garamond',serif;font-size:20px;font-weight:400;margin:28px 0 14px;padding-bottom:8px;border-bottom:1px solid var(--brd);color:var(--au-l);}
.sd-story{margin-bottom:20px;}.sd-story p{font-size:13.5px;color:var(--t2);line-height:1.8;margin-bottom:12px;}
.sd-features{display:flex;flex-direction:column;gap:10px;margin-bottom:20px;}
.sd-feat{display:flex;align-items:flex-start;gap:10px;font-size:13px;color:var(--t2);line-height:1.6;}
.sd-feat-dot{width:6px;height:6px;border-radius:50%;background:var(--au);margin-top:7px;flex-shrink:0;}
.sd-cta{padding:24px 0 8px;text-align:center;border-top:1px solid var(--brd);margin-top:28px;}
/* â•â•â• v20: LEGAL MODAL â•â•â• */
.leg-modal{max-width:720px;max-height:85vh;background:var(--navy);border:1px solid var(--brd);border-radius:10px;margin:auto;display:flex;flex-direction:column;overflow:hidden;}
.leg-header{display:flex;align-items:center;gap:10px;padding:16px 24px;border-bottom:1px solid var(--brd);flex-shrink:0;}.leg-header .fv-close{margin-left:auto;}
.leg-title{font-family:'Cormorant Garamond',serif;font-size:16px;font-weight:500;color:var(--t1);}
.leg-body{padding:24px 32px;overflow-y:auto;font-size:13px;color:var(--t2);line-height:1.8;-webkit-overflow-scrolling:touch;}
.leg-body h2{font-family:'Cormorant Garamond',serif;font-size:24px;font-weight:500;color:var(--au);margin:0 0 8px;}
.leg-body h3{font-size:14px;font-weight:600;color:var(--t1);margin:24px 0 8px;letter-spacing:.3px;}
.leg-body p{margin:0 0 12px;color:var(--t3);}
.leg-body .leg-up{font-size:11px;color:var(--t4);margin-bottom:24px;padding-bottom:16px;border-bottom:1px solid var(--brd);}
.leg-body strong{color:var(--t1);font-weight:600;}
.sd-report-frame{border:1px solid var(--brd);border-radius:8px;overflow:hidden;margin-bottom:8px;}
.sd-wa-frame{border:1px solid var(--brd);border-radius:8px;overflow:hidden;margin-bottom:16px;}

/* â•â•â• v16: BANK DIRECTORY â•â•â• */
.sd-banks{display:grid;grid-template-columns:1fr;gap:6px;margin-bottom:8px;}
.sd-bank{padding:14px 16px;border:1px solid var(--brd);border-radius:6px;background:var(--navy2);transition:border-color .3s;}.sd-bank:hover{border-color:var(--au-d);}
.sd-bank-top{display:flex;align-items:center;gap:10px;margin-bottom:6px;}
.sd-bank-flag{font-size:20px;flex-shrink:0;}
.sd-bank-name{font-size:14px;font-weight:500;}
.sd-bank-loc{font-size:10px;color:var(--t3);letter-spacing:.3px;margin-top:1px;}
.sd-bank-spec{font-size:12px;color:var(--t2);line-height:1.6;padding-left:30px;}

/* â•â•â• v16: QUARTERLY REPORT â€” FT style â•â•â• */
.qr{background:#FFF8F0;color:#1A1A22;font-family:'Plus Jakarta Sans','Inter',sans-serif;padding:0;}
.qr-masthead{display:flex;justify-content:space-between;align-items:center;padding:16px 24px;border-bottom:2px solid #1A1A22;background:#FFF8F0;}
.qr-mast-left{display:flex;align-items:center;gap:12px;}
.qr-mast-tag{font-size:9px;letter-spacing:1.5px;text-transform:uppercase;color:#fff;background:#1A1A22;padding:4px 10px;font-weight:600;}
.qr-mast-date{font-size:12px;color:#666;}.qr-mast-id{font-size:11px;color:#999;}
.qr-hero{display:flex;justify-content:space-between;align-items:flex-end;padding:24px;border-bottom:1px solid #E5DDD0;background:#FFF8F0;}
.qr-hero-left{}.qr-hero-label{font-size:9px;letter-spacing:1.5px;text-transform:uppercase;color:#999;margin-bottom:4px;}.qr-hero-val{font-family:'Cormorant Garamond',serif;font-size:36px;font-weight:400;line-height:1;margin-bottom:4px;}.qr-hero-chg{font-size:14px;font-weight:500;}
.qr-hero-kpis{display:grid;grid-template-columns:repeat(4,1fr);gap:16px;}
.qr-hero-kpi{text-align:center;}.qr-hero-kv{font-family:'Cormorant Garamond',serif;font-size:18px;font-weight:400;}.qr-hero-kl{font-size:8px;letter-spacing:.8px;text-transform:uppercase;color:#999;margin-top:1px;}
.qr-section{padding:16px 24px;border-bottom:1px solid #E5DDD0;}
.qr-sh{font-family:'Cormorant Garamond',serif;font-size:16px;font-weight:500;margin-bottom:10px;color:#1A1A22;}
.qr-chart-leg{display:flex;gap:16px;margin-top:4px;}.qr-leg{display:flex;align-items:center;gap:4px;font-size:10px;color:#999;}
.qr-mc-note{font-size:11px;color:#999;font-style:italic;margin-bottom:8px;}
.qr-mc-bands{display:flex;gap:16px;flex-wrap:wrap;margin-top:6px;}.qr-mc-band{display:flex;align-items:center;gap:4px;font-size:11px;color:#666;}.qr-mc-band strong{color:#1A1A22;}
.qr-stress{display:flex;flex-direction:column;gap:6px;}
.qr-stress-row{display:flex;align-items:center;justify-content:space-between;padding:10px 14px;background:#fff;border:1px solid #E5DDD0;border-radius:4px;}
.qr-stress-name{font-size:13px;font-weight:500;flex:1;}.qr-stress-vals{display:flex;gap:14px;}
.qr-sv{font-size:13px;font-weight:600;text-align:center;min-width:48px;}.qr-sv.red{color:#C0392B;}.qr-sv.grn{color:#27AE60;}
.qr-svl{display:block;font-size:8px;font-weight:400;color:#999;letter-spacing:.8px;text-transform:uppercase;margin-top:1px;}
.qr-disc{padding:12px 24px;font-size:9px;color:#bbb;text-align:center;font-style:italic;background:#FFF8F0;}
.qr-prose{font-size:13px;color:#444;line-height:1.8;}.qr-prose-sm{font-size:11.5px;color:#666;line-height:1.7;}
.qr-tbl-hdr{background:#F5F2ED;}.qr-tbl-row{font-size:11px;}
.qr-peer-grid{display:flex;flex-direction:column;gap:6px;margin-bottom:10px;}
.qr-peer-row{display:flex;align-items:center;gap:8px;font-size:12px;}
.qr-peer-label{min-width:100px;color:#666;font-size:11px;}.qr-peer-bar-wrap{flex:1;height:10px;background:#F0EDE8;border-radius:5px;overflow:hidden;}.qr-peer-bar{height:100%;border-radius:5px;transition:width .6s;}.qr-peer-val{min-width:48px;text-align:right;font-weight:500;color:#333;}.qr-peer-val.bold{font-weight:700;color:#0D4F8B;}
.qr-risk-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;}
.qr-risk-item{padding:14px;background:#fff;border:1px solid #E5DDD0;border-radius:6px;}
.qr-risk-top{display:flex;align-items:baseline;gap:6px;margin-bottom:4px;}.qr-risk-val{font-family:'Cormorant Garamond',serif;font-size:22px;font-weight:400;color:#1A1A22;}.qr-risk-ref{font-size:10px;color:#27AE60;font-weight:600;letter-spacing:.3px;}
.qr-risk-label{font-size:10px;font-weight:600;letter-spacing:.5px;text-transform:uppercase;color:#999;margin-bottom:2px;}.qr-risk-note{font-size:10px;color:#888;line-height:1.4;}

.qr-actions{display:flex;flex-direction:column;gap:10px;}
.qr-action{display:flex;gap:12px;padding:14px;background:#fff;border:1px solid #E5DDD0;border-radius:6px;}
.qr-action-icon{font-size:16px;flex-shrink:0;margin-top:2px;color:#27AE60;}.qr-action-icon.warn{color:#D4845A;}
.qr-action-t{font-size:13px;font-weight:600;color:#1A1A22;margin-bottom:3px;}.qr-action-d{font-size:12px;color:#666;line-height:1.6;}

/* â•â•â• v16: BENCHMARK VIZ â•â•â• */
.bv{margin:16px 0;}
.bv-tabs{display:flex;gap:6px;margin-bottom:12px;}.bv-tab{padding:8px 18px;border:1px solid var(--brd);background:none;color:var(--t3);font-family:inherit;font-size:11px;letter-spacing:.5px;cursor:pointer;border-radius:4px;transition:all .2s;}.bv-tab.on{background:var(--au);color:var(--navy);border-color:var(--au);}
.bv-chart{border:1px solid var(--brd);border-radius:8px;padding:16px;background:var(--navy);}
.bv-verdict{margin-top:12px;display:flex;flex-direction:column;gap:4px;}
.bv-bad{color:#D4845A;font-size:14px;font-weight:600;}.bv-good{color:#3DAA6D;font-size:14px;font-weight:600;}
.bv-exp{font-size:12px;color:var(--t3);}

/* â•â•â• RESPONSIVE â€” v13: proper mobile with hamburger â•â•â• */
@media(max-width:1024px){
  .hero-h1{font-size:38px;}.hero-c{margin-left:24px;}.svc4,.hw-steps{grid-template-columns:repeat(2,1fr);}.fdr{grid-template-columns:1fr;gap:32px;}.fdr-frame{max-width:220px;aspect-ratio:1;}.brd-cards{grid-template-columns:1fr;}.hero-stats{grid-template-columns:repeat(2,auto);gap:20px;}.ft-in{grid-template-columns:1fr;gap:24px;}.we-grid{grid-template-columns:1fr;}.we-results{grid-template-columns:1fr;}.we-fee-compare{flex-wrap:wrap;gap:8px;}.portal-kpis{grid-template-columns:repeat(2,1fr);}.portal-meta{display:none;}.sp-results{grid-template-columns:repeat(2,1fr);}.pv-cards{grid-template-columns:1fr;}.fv-modal{max-width:100%;max-height:100vh;border-radius:0;}.leg-modal{max-width:100%;max-height:100vh;border-radius:0;margin:0;}.art-modal{max-width:100%;max-height:100vh;border-radius:0;margin:0;}.art-body{padding:8px 28px 36px;}.leg-body{padding:20px;}.qr-hero{flex-direction:column;gap:16px;align-items:flex-start;}.qr-hero-kpis{grid-template-columns:repeat(2,1fr);}.qr-stress-vals{gap:8px;}.sd-body{padding:0 20px 20px;}.mr-hero{flex-direction:column;gap:16px;align-items:flex-start;}.mr-hero-kpis{grid-template-columns:repeat(4,1fr);}.mr-two-col{grid-template-columns:1fr;}.qr-risk-grid{grid-template-columns:repeat(2,1fr);}.acc-grid{grid-template-columns:repeat(auto-fill,minmax(180px,1fr));}.acc-grid.lg{grid-template-columns:repeat(auto-fill,minmax(160px,1fr));}
}
@media(max-width:768px){
  .nv-desk{display:none!important;}.nv-mob{display:flex!important;}
}
@media(max-width:640px){
  .nv{padding:12px 16px;}.hero{padding:90px 20px 50px;}.hero-c{margin-left:0;}.hero-h1{font-size:30px;}.sec{padding:60px 20px;}.sec-h2{font-size:28px;}.svc4,.hw-steps{grid-template-columns:1fr;}.ky{width:96vw;height:92vh;border-radius:8px;}.hero-stats{grid-template-columns:repeat(2,auto);gap:16px;}.hero-stat-n{font-size:26px;}.ft{padding:32px 16px 0;}.ft-links{grid-template-columns:1fr;gap:12px;}.ft-bot{flex-direction:column;gap:6px;}.ft-sep{display:none;}.calc{padding:16px;}.we-cv,.we-sl-v{font-size:20px;}.we-fee-compare{flex-direction:column;gap:10px;}.we-fee-arrow{transform:rotate(90deg);}.we-bands{gap:3px;}.we-band{padding:5px 8px;font-size:10px;}.portal-kpis{grid-template-columns:repeat(2,1fr);}.portal-body{padding:14px;}.portal-pr{grid-template-columns:1fr auto;}.we-presets{flex-wrap:wrap;}.sp-results{grid-template-columns:repeat(2,1fr);}.sp-timeline{padding-left:40px;}.sp-marker{left:-40px;width:30px;height:30px;}.hero-diamond{display:none;}.hero-line{display:none;}.pv-card-inner{padding:20px 16px;}.pv-card-stats{flex-wrap:wrap;}.fv-overlay{padding:0;}.fv-modal{border-radius:0;max-height:100vh;}.leg-modal{border-radius:0;max-height:100vh;}.art-modal{border-radius:0;max-height:100vh;}.art-body{padding:8px 20px 32px;}.art-h1{font-size:24px;}.art-content blockquote{font-size:16px;}.leg-body{padding:16px 20px;}.leg-body h2{font-size:20px;}.leg-body h3{font-size:13px;}.lang-card{padding:18px 20px;gap:14px;}.lang-card:hover{padding-left:20px;}.lang-card-icon{font-size:26px;}.lang-card-name{font-size:18px;}.lang-tip{position:static;transform:none;opacity:1;width:auto;box-shadow:none;border:none;padding:10px 0 0;margin-top:6px;border-top:1px solid var(--brd);pointer-events:auto;}.lang-tip::after{display:none;}.qr-hero-val{font-size:28px;}.qr-hero-kpis{grid-template-columns:repeat(2,1fr);gap:8px;}.qr-stress-row{flex-direction:column;gap:8px;align-items:flex-start;}.qr-stress-vals{flex-wrap:wrap;gap:8px;}.sd-body{padding:0 16px 16px;}.sd-test{padding:20px;margin:-20px -16px 20px;}.sd-bank-spec{padding-left:0;margin-top:6px;}.mr-hero{flex-direction:column;gap:12px;}.mr-hero-val{font-size:28px;}.mr-hero-kpis{grid-template-columns:repeat(2,1fr);gap:8px;}.mr-mast{flex-direction:column;gap:6px;align-items:flex-start;}.mr-section{padding:12px 16px;}.mr-two-col{padding:12px 16px;grid-template-columns:1fr;gap:16px;}.mr-tbl-hdr,.mr-tbl-row{font-size:10px;}.mr-tbl-hdr .mr-th:nth-child(2){display:none;}.mr-tbl-row .mr-td:nth-child(2){display:none;}.qr-risk-grid{grid-template-columns:1fr;}.qr-section{padding:12px 16px;}.acc-grid,.acc-grid.lg{grid-template-columns:repeat(2,1fr);}
  .ck-bar{flex-direction:column;padding:14px 16px;gap:10px;text-align:center;}.ck-acts{justify-content:center;}.wa-float{bottom:16px;right:16px;width:46px;height:46px;}.wa-float svg{width:22px;height:22px;}.hero-fq{margin-bottom:24px;}
}
/* â•â•â• v26: COOKIE CONSENT â•â•â• */
.ck-bar{position:fixed;bottom:0;left:0;right:0;z-index:999;background:var(--navy2);border-top:1px solid var(--brd);padding:14px 24px;display:flex;align-items:center;justify-content:space-between;gap:16px;animation:slideUp .4s ease both;}
@keyframes slideUp{from{transform:translateY(100%);opacity:0}to{transform:translateY(0);opacity:1}}
.ck-txt{font-size:12px;color:var(--t3);line-height:1.5;flex:1;}
.ck-acts{display:flex;gap:8px;flex-shrink:0;}
.ck-acc{padding:8px 20px;background:var(--au);color:var(--navy);border:none;font-family:inherit;font-size:12px;font-weight:600;cursor:pointer;border-radius:4px;letter-spacing:.3px;transition:background .2s;}.ck-acc:hover{background:var(--au-l);}
.ck-dec{padding:8px 16px;background:none;border:1px solid var(--brd);color:var(--t3);font-family:inherit;font-size:12px;cursor:pointer;border-radius:4px;transition:all .2s;}.ck-dec:hover{border-color:var(--t3);color:var(--t2);}

/* â•â•â• v26: WHATSAPP FLOAT â•â•â• */
.wa-float{position:fixed;bottom:24px;right:24px;z-index:900;width:52px;height:52px;border-radius:50%;background:#25D366;display:flex;align-items:center;justify-content:center;box-shadow:0 4px 16px rgba(37,211,102,.35);transition:transform .2s,box-shadow .2s;cursor:pointer;text-decoration:none;}.wa-float:hover{transform:scale(1.08);box-shadow:0 6px 24px rgba(37,211,102,.5);}

@media(prefers-reduced-motion:reduce){
  .sec,.cta,.hero,.lang-card,.lang-tip,.ky,.ky-overlay,.ck-bar{transition:none!important;animation:none!important;opacity:1!important;transform:none!important;}
}
`;
