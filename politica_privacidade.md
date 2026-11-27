# Política de Privacidade do BMSViewer

App: BMSViewer, publicado no Google Play como "BMS Battery Monitor: LiFePO4" (pacote local.bmsviewer.app).

Desenvolvedor: Alan Spohr Perius

Data de vigência: 2026-11-27

Contato: alan.perius.mv@gmail.com

O BMSViewer é um aplicativo Android que se conecta, por Bluetooth Low Energy (BLE), ao BMS (sistema de gerenciamento de bateria) de baterias JK, LiTime, JBD e Daly (só leitura; LiTime, JBD e Daly são experimentais), e lê aparelhos Victron (experimental) pelo anúncio Bluetooth, sem conectar e sem enviar nada ao aparelho; para isso precisa da chave de criptografia do aparelho, obtida no VictronConnect. O app mostra os dados na tela. Opcionalmente, você pode ligar o monitoramento remoto para enviar suas leituras, criptografadas de ponta a ponta, a outro celular seu ou de alguém que você autorizou (seção 5). O aplicativo só envia pedidos de leitura (no BMS JK: informações do dispositivo e das células; na bateria LiTime: um pedido de status; nos BMS JBD e Daly: só pedidos de leitura; nos aparelhos Victron: nada é enviado) e ativa notificações. Ele nunca altera nenhuma configuração do BMS e nunca pede pareamento Bluetooth; se o Android pedir, recuse.

Opcionalmente, você também pode aceitar as estatísticas de uso (seção 6). Elas vêm desligadas por padrão, não levam nome, MAC nem leituras, e só são enviadas depois que você aceita.


## 1. Resumo

- O monitoramento remoto e as estatísticas de uso são opcionais e vêm desligados. Se você não ligar o monitoramento remoto nem aceitar as estatísticas de uso, o aplicativo não envia dados para servidores do desenvolvedor nem de terceiros. Suas leituras ficam no seu celular, a menos que você as exporte ou ligue o monitoramento remoto. A leitura da bateria por Bluetooth funciona offline.
- Se você ligar o monitoramento remoto, suas leituras são enviadas criptografadas de ponta a ponta ao servidor do desenvolvedor. As chaves de criptografia existem só no seu celular e nos celulares que você autorizar; por isso o desenvolvedor não consegue ler suas leituras.
- O aplicativo declara as permissões de internet (INTERNET) e de estado da rede (ACCESS_NETWORK_STATE) só para o monitoramento remoto e para as estatísticas de uso opcionais. Elas não são usadas para mais nada: sem anúncios e sem relatórios de falha.
- Sem anúncios e sem SDK de relatório de falhas. A única ferramenta de medição são as estatísticas de uso opcionais do Google Analytics for Firebase (seção 6), que você pode recusar ou desligar a qualquer momento.
- Sem conta, cadastro ou login. Sem compras.
- As estatísticas de uso, se você aceitar, não levam nome, MAC ou endereço Bluetooth, nem leituras da bateria, e não usam o ID de publicidade (seção 6).

## 2. Dados que o app lê

Ao se conectar ao BMS (JK, LiTime, JBD ou Daly) ou ao ler um aparelho Victron, o aplicativo lê:

- Leitura da bateria: carga (SOC), tensão, corrente, potência e capacidade restante.
- Tensão de cada célula e diferença entre células.
- Temperaturas (vários sensores). No histórico, o app guarda a temperatura máxima.
- Diagnóstico: estado da permissão e do Bluetooth, intensidade do sinal, variante de firmware e registro da conexão com textos fixos. Essa tela não é gravada no aparelho.
- Aparelhos Victron: o aplicativo lê o anúncio Bluetooth do aparelho, sem conectar e sem enviar nada a ele. Para decifrar o anúncio, usa a chave de criptografia do aparelho, que você obtém no VictronConnect e informa no app.
- Um identificador opaco da bateria, que pode ser o endereço Bluetooth do BMS. Serve para reconhecer a bateria salva e nunca é exibido no app.

O aplicativo não usa sua localização, contatos, fotos, microfone, câmera nem identificador de publicidade. Só as estatísticas de uso opcionais, se você aceitar, levam a região aproximada que o Google deduz do endereço IP (seção 6). O fuso horário e a região do idioma são lidos no celular para a regra europeia (seção 6); o app não os envia. Se você aceitar as estatísticas, o SDK do Google envia por conta própria o idioma do celular e pode enviar o fuso horário (seção 6). Ele só cria um arquivo quando você exporta o histórico em CSV (seção 5). Se o monitoramento remoto estiver ligado, o app também usa um código aleatório de canal e chaves de criptografia (seção 5).


## 3. Permissões e por que são necessárias

- Dispositivos próximos, buscar (BLUETOOTH_SCAN, Android 12 ou superior): encontrar o BMS. Declarada com "neverForLocation": o escaneamento não é usado para deduzir sua localização.
- Dispositivos próximos, conectar (BLUETOOTH_CONNECT, Android 12 ou superior): conectar ao BMS escolhido.
- Bluetooth e Bluetooth admin (BLUETOOTH, BLUETOOTH_ADMIN), só Android 11 ou inferior: equivalentes antigas das duas anteriores.
- Localização aproximada e precisa (ACCESS_COARSE_LOCATION, ACCESS_FINE_LOCATION), só Android 11 ou inferior: o Android exige essa permissão para escanear Bluetooth nessas versões. O app não lê nem guarda sua localização.
- Serviço em primeiro plano (FOREGROUND_SERVICE, FOREGROUND_SERVICE_CONNECTED_DEVICE): manter a conexão Bluetooth com o BMS enquanto o app está em segundo plano, em dois casos (e, se você ligar o monitoramento remoto, também manter o app em execução para que as leituras criptografadas sejam enviadas no intervalo escolhido). (1) Por padrão ("Manter sempre conectado" desligado): se uma leitura ao vivo estiver em andamento quando você sai do app, a conexão é mantida por uma carência de cerca de 60 segundos; depois o app fecha a conexão e o serviço para. (2) Com "Manter sempre conectado" ligado: a conexão é mantida até você desligar a opção, tocar em Desconectar na notificação ou tocar em Parar no app. Quando este celular começa a enviar, o app liga essa opção e a trava nos Ajustes enquanto está enviando. Se você pausar o envio, ela continua ligada, mas pode ser desligada nos Ajustes; ao parar e apagar o envio, ela volta ao que era antes.
- Notificações (POST_NOTIFICATIONS): usada só para a notificação desse serviço em primeiro plano. Ela mostra o percentual de carga e a potência e pode aparecer na tela de bloqueio. Se você negar a permissão, a conexão continua, mas sem aviso visível. O app não envia outras notificações; os alertas aparecem só dentro do app.
- Internet (INTERNET) e estado da rede (ACCESS_NETWORK_STATE): usadas só se você ligar o monitoramento remoto (para enviar e receber leituras criptografadas e verificar se o celular está online) ou se aceitar as estatísticas de uso (seção 6). Não são usadas de outra forma. O app não pede a permissão do ID de publicidade (AD_ID).
- Manter ativo (WAKE_LOCK): um wake lock parcial, mantido por no máximo 75 segundos. Cobre os 60 segundos de tolerância em segundo plano, a liberação do enlace Bluetooth e um ciclo de reconexão. É mantido mesmo com "Manter sempre conectado" desligado.

O app não registra nenhum link no Android: nenhum link abre o aplicativo. Ele apenas abre a tela de configurações do sistema para o aplicativo, pelo recurso padrão do Android.


## 4. O que fica guardado no seu aparelho

Tudo o que o app guarda no celular fica no armazenamento privado do app:

- Baterias salvas (até 10), cada uma com um identificador opaco (que pode ser o endereço Bluetooth, nunca exibido) e um apelido que você escolhe; a bateria fixada.
- Idioma, tema (automático, escuro ou claro), limites de alerta e a opção "Manter sempre conectado".
- A última leitura de cada bateria.
- Histórico de leituras por bateria: SOC, tensão, corrente, potência, diferença entre células, tensão mínima e máxima de célula e temperatura máxima. Guardado por minuto e, após 48 horas, agrupado em intervalos de 15 minutos, por até 30 dias, limitado a cerca de 2,5 MB.
- Chave de criptografia dos aparelhos Victron: guardada no armazenamento seguro do Android (Android Keystore), só no seu celular, e nunca enviada a lugar nenhum.
- Aparelhos Victron salvos: apelido e capacidade, guardados no celular.
- No celular que vê: uma cópia local, já descriptografada, das leituras recebidas nos últimos 7 dias, para mostrar a última leitura sem internet.
- Se você usar o monitoramento remoto: a opção ligada/desligada, a lista de celulares autorizados, os códigos aleatórios de canal e de visualizador e as chaves de criptografia. O backup do Android continua desativado; nada disso é copiado para a nuvem.
- Sua escolha sobre as estatísticas de uso (ligadas, desligadas ou ainda não escolhidas). Enquanto estão ligadas, o SDK do Google Analytics também guarda, no armazenamento privado do app, o identificador próprio desta instalação (o ID da instância do app).

Fora a chave do Victron (no Keystore), o app não criptografa os dados em repouso; eles ficam no armazenamento privado do app no Android. O backup automático do Android (nuvem e transferência entre aparelhos) está desativado para o app.


## 5. Exportação, compartilhamento e monitoramento remoto

- Com o monitoramento remoto desligado, o servidor do desenvolvedor não recebe nenhum dado. O desenvolvedor vê apenas as estatísticas de uso opcionais, no Google Analytics, se você as aceitou (seção 6).
- Com ele ligado, o celular que envia criptografa cada leitura no próprio celular antes de enviá-la. Os celulares autorizados baixam e descriptografam. As chaves ficam só nesses celulares; o desenvolvedor não consegue ler as leituras.
- O que é enviado, tudo criptografado de ponta a ponta: carga, tensão, corrente e potência; capacidade, carga restante e a estimativa de duração; número de células, a menor e a maior tensão e a diferença; temperaturas; alarmes e a marca do BMS; no banco, quantas baterias são, quantas foram lidas e a menor carga. Deste celular: se está na tomada, carga e temperatura, tipo de internet, se o Bluetooth está lendo a bateria ou foi parado, o intervalo de envio, economia de bateria, se as notificações estão permitidas, último reinício, o número de reinícios do celular (um contador do Android, usado só para saber se o celular reiniciou; sozinho, não identifica o aparelho), tempo desde que ligou, quantidade de leituras guardadas, versão do app e se está enviando. E o nome que cada celular autorizado escolher. Não é enviado: localização por GPS, nome, e-mail, endereço Bluetooth da bateria, senha da bateria, apelido da bateria nem a chave dos aparelhos Victron.
- O que o servidor guarda: as leituras criptografadas; os códigos de canal e de visualizador, guardados só como hash; e metadados de pareamento e de uso (quais celulares visualizadores estão ligados a um canal, entradas de visualizadores, e horários, números de sequência, época da chave e tamanhos dos envios). O servidor não tem conta, e-mail, nome, identificador do aparelho, identificador de publicidade nem localização.
- Endereço IP: o provedor de hospedagem (Railway, EUA) pode registrar o endereço IP em seus logs técnicos; o app e o servidor não armazenam o endereço IP. Para limitar abusos, o servidor usa apenas um hash de curta duração, com sal diário, do prefixo do endereço IP, mantido na memória para limitar a taxa de requisições.
- O servidor do monitoramento remoto fica na Railway, que trata os dados em nome do desenvolvedor. Nada nele é vendido nem usado para publicidade ou análise de uso. As estatísticas de uso opcionais (seção 6) não passam por esse servidor; vão para o Google.
- O pareamento é feito só por um código que você digita, confirmado com um número de verificação nos dois celulares. Você decide quem pode ver: só as pessoas que você autorizar. Remover um visualizador revoga o acesso dele quando o servidor confirma; se não confirmar, o app avisa.
- Na tela de Histórico você pode exportar um arquivo CSV pela folha de compartilhamento do Android. Isso só acontece quando você toca em exportar. O app cria um arquivo temporário para o compartilhamento. O arquivo contém horários em UTC e as leituras, sem identificador da bateria, apelido nem endereço Bluetooth.
- O app, por conta própria, não envia o CSV a lugar nenhum. Você escolhe o app de destino e, a partir daí, vale a política de privacidade desse app.
- O app não vende dados. Além das estatísticas de uso opcionais enviadas ao Google (seção 6), ele não compartilha dados com terceiros por conta própria.

## 6. Estatísticas de uso opcionais (Google Analytics for Firebase)

As estatísticas de uso são opcionais e vêm desligadas por padrão. O app pergunta na primeira abertura e também pergunta a quem atualiza de uma versão que não as tinha. Você pode mudar sua escolha a qualquer momento em Ajustes > Estatísticas de uso. Nada é enviado antes de você aceitar.


### O que é enviado, só depois de você aceitar

- Quais telas e recursos você usa, por exemplo as telas que abre, o resultado de uma busca Bluetooth, exportar ou apagar o histórico, mudar um alerta e mudar o idioma, o tema ou a opção "Manter sempre conectado". Cada um é um evento com valores fixos de uma lista fechada; não há texto livre.
- A marca e a família das baterias que você adiciona, verifica ou remove (por exemplo JK, LiTime, JBD, Daly, Victron); quantas baterias você tem salvas, em faixas; se você usa um banco de baterias, quantas baterias ele tem, o tipo de ligação e se há marcas misturadas; e se você usa o monitoramento remoto (papel, intervalo de envio e resultado do pareamento, como códigos fixos).
- Códigos de resultado e de erro de uma lista fixa (por exemplo Bluetooth desligado, bateria não encontrada, chave salva ou não). Nunca uma mensagem de erro nem texto produzido pelo celular ou pela bateria.
- Algumas configurações e contagens do app, como propriedades de usuário com valores fixos: marcas das baterias, número de baterias e de alertas em faixas, se você usa banco ou Victron, papel no monitoramento remoto, "Manter sempre conectado", idioma e tema.
- O que o Google Analytics for Firebase coleta por conta própria: o ID da instância do app (um código aleatório desta instalação do app neste celular), o ID de instalação do Firebase, a versão do app, o modelo do celular e a versão do Android, o idioma do celular (com a região, por exemplo pt-BR), o fuso horário, a região aproximada que o Google deduz do endereço IP da conexão e eventos automáticos, como primeira abertura, início de sessão, tempo de engajamento, atualização do app ou do Android e remoção do app.

### O que nunca é enviado

Nunca são enviados: seu nome ou e-mail; o endereço Bluetooth ou MAC de qualquer bateria ou aparelho; leituras da bateria (carga, tensão, corrente, potência, temperatura, tensão das células) e o conteúdo de arquivos CSV exportados; apelidos das baterias; senhas e chaves, inclusive a chave do Victron; códigos, links, identificadores de canal e endereço do servidor do monitoramento remoto; localização por GPS, contatos ou número de telefone; e o ID de publicidade do Android.


### Sem publicidade

As estatísticas servem só para entender quais recursos e marcas de bateria são usados, para melhorar o app. A permissão do ID de publicidade (AD_ID) foi removida do app, os sinais do Google estão desligados, a personalização de anúncios está desligada, a coleta de dados granulares de localização e do aparelho está desligada, e a propriedade não está ligada ao Google Ads. Não há criação de perfil para publicidade.


### Quem recebe e a base legal

Os dados vão para o Google Analytics for Firebase, um serviço do Google, que os trata em nome do desenvolvedor. O Google pode tratá-los em países diferentes do seu, inclusive nos Estados Unidos. Como os dados ficam ligados a um código aleatório da sua instalação, o desenvolvedor os trata como dados pessoais. A base legal é o seu consentimento (LGPD, art. 7º, I; GDPR, art. 6(1)(a)), que você pode retirar a qualquer momento, sem afetar o que foi feito antes.


### Como desligar

Em Ajustes > Estatísticas de uso, desligue a chave. O app para de coletar na hora e troca o ID da instância do app por um novo. Desligar não apaga o que já foi enviado: esses dados ficam no Google Analytics até o fim do prazo de retenção abaixo. Depois que o código é trocado, o desenvolvedor não consegue mais achar os dados antigos. Se quiser que o que já foi enviado seja apagado, use antes Pedir exclusão (abaixo).


### Retenção

No Google Analytics, os dados por usuário e por evento ligados ao código ficam por 14 meses e depois são apagados. Relatórios agregados, com contagens gerais e sem o código, podem ficar mais tempo.


### Pedir exclusão e seus direitos

Para pedir a exclusão do que já foi enviado, abra Ajustes > Estatísticas de uso > Pedir exclusão. Isso só funciona enquanto as estatísticas estão ligadas. O app abre seu aplicativo de e-mail com uma mensagem pronta para o e-mail de contato abaixo, com o código desta instalação (o ID da instância do app); você mesmo envia. Com esse código, o desenvolvedor consegue achar e apagar os dados usando as ferramentas de exclusão do Google Analytics. Use isso antes de desligar as estatísticas: depois que o código é trocado, esses dados não podem mais ser encontrados e são apagados ao fim dos 14 meses.

Como as estatísticas não levam nome nem e-mail, o desenvolvedor não consegue achá-las só pelo seu nome ou e-mail. Você também pode, pela LGPD (art. 18) e, quando se aplicar, pelo GDPR, pedir confirmação, acesso, correção, exclusão, portabilidade ou oposição, e retirar seu consentimento, escrevendo para o e-mail de contato abaixo; e pode reclamar à autoridade de proteção de dados (no Brasil, a ANPD).


### Monitoramento remoto e as estatísticas

- Fora do Espaço Econômico Europeu (EEE), do Reino Unido e da Suíça: criar um canal novo de monitoramento remoto exige aceitar as estatísticas de uso. O app pergunta de novo cada vez que você abre a tela do monitoramento remoto; recusar bloqueia só canais novos. Um canal de monitoramento remoto que já funciona não é parado por uma atualização do app. Se você desligar as estatísticas em Ajustes, o monitoramento remoto para neste celular (envio ou visualização), com um aviso, até você ligar de novo. Desligar não apaga os dados do monitoramento remoto no servidor (seção 7).
- Dentro do EEE, do Reino Unido e da Suíça: o monitoramento remoto não exige as estatísticas de uso, e desligar as estatísticas não afeta o monitoramento remoto. O app decide isso no próprio celular, sem enviar nada: trata o celular como europeu quando o fuso horário é europeu, quando a região do idioma é de um desses países, ou quando não consegue ler nenhum dos dois. Por isso a regra europeia também vale em alguns países vizinhos que usam fuso europeu.

## 7. Retenção e exclusão

- Estatísticas de uso enviadas ao Google: veja a seção 6 (14 meses para os dados ligados ao código da instalação; como pedir exclusão).
- O histórico é mantido por no máximo 30 dias e limitado a cerca de 2,5 MB.
- "Apagar histórico desta bateria" apaga só o histórico daquela bateria.
- O app só remove uma bateria salva da lista quando a marca dela não é reconhecida (botão Remover na tela de erro). Na tela da chave de um aparelho Victron, "Apagar a chave" apaga a chave e o aparelho Victron salvo. Para remover as outras baterias salvas, identificadores, apelidos, últimas leituras e configurações, limpe os dados do app nas configurações do Android ou desinstale o app.
- Dados locais: você os apaga como descrito acima; o desenvolvedor não tem acesso a eles.
- Dados remotos, leituras criptografadas: apagadas do servidor automaticamente após 7 dias.
- Dados remotos, registro do canal e metadados (vínculos entre celulares, entradas de visualizadores, horários, números de sequência, época da chave e tamanhos dos envios): mantidos até 180 dias sem receber envio e depois apagados (7 dias, se o canal nunca recebeu nenhum envio e nenhum visualizador foi autorizado). Visualizadores sem uso por 180 dias também são apagados. Pareamentos expirados e visualizadores pendentes são apagados após 1 hora.
- "Parar e apagar dados do servidor" no app apaga a cópia do servidor assim: se o servidor aceita o pedido, apaga na hora; se não há internet, o pedido fica pendente e o app tenta de novo; se o acesso for recusado (o celular perdeu o acesso), o app apaga os dados do celular mas não consegue confirmar no servidor, e a cópia de lá some sozinha pelo prazo de retenção. Remover um visualizador revoga o acesso dele quando o servidor confirma; se não confirmar, o app avisa. O servidor não guarda e-mail, nome nem outra identificação sua, então o desenvolvedor não tem como localizar seus dados a partir de um e-mail: apague pelo app ou espere a expiração automática.
- Não há backups do banco de dados configurados (nem cópias agendadas, nem recuperação a um ponto no tempo). Se isso mudar, esta política é atualizada antes.
- Um CSV exportado é um arquivo separado, fora do app; apague-o você mesmo no local onde o salvou ou enviou.

## 8. Crianças

O aplicativo não é direcionado a crianças e não trata conscientemente dados de crianças.


## 9. Alterações

Mudanças nesta política serão publicadas nesta página com nova data de vigência. Data de vigência 2026-11-27: incluídas as estatísticas de uso opcionais (Google Analytics for Firebase), seção 6, e a relação delas com o monitoramento remoto. Data de vigência 2026-11-22: incluídos o monitoramento remoto opcional e a leitura de aparelhos Victron.


## 10. Contato

alan.perius.mv@gmail.com

---

