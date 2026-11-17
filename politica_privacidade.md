# Política de Privacidade do BMSViewer

Desenvolvedor: Alan Spohr Perius
Data de vigência: 2026-11-16
Contato: alan.perius.mv@gmail.com

O BMSViewer é um aplicativo Android que se conecta, por Bluetooth Low Energy (BLE), ao BMS (sistema de gerenciamento de bateria) de uma bateria que usa BMS JK e mostra os dados na tela. O aplicativo só envia pedidos de leitura (informações do dispositivo e das células) e ativa notificações. Ele nunca altera nenhuma configuração do BMS.

## 1. Resumo

- Por conta própria, o aplicativo não envia dados para servidores do desenvolvedor nem de terceiros. Suas leituras ficam no seu celular, a menos que você as exporte.
- O aplicativo não declara a permissão de internet (INTERNET).
- Sem anúncios, sem análise de uso (analytics) e sem SDK de relatório de falhas.
- Sem conta, cadastro ou login. Sem compras.

## 2. Dados que o app lê

Ao se conectar ao BMS, o aplicativo lê:

- Leitura da bateria: carga (SOC), tensão, corrente, potência e capacidade restante.
- Tensão de cada célula e diferença entre células.
- Temperaturas (vários sensores). No histórico, o app guarda a temperatura máxima.
- Diagnóstico: estado da permissão e do Bluetooth, intensidade do sinal, variante de firmware e registro da conexão com textos fixos. Essa tela não é gravada no aparelho.
- Um identificador opaco da bateria, que pode ser o endereço Bluetooth do BMS. Serve para reconhecer a bateria salva e nunca é exibido no app.

O aplicativo não usa sua localização, contatos, fotos, microfone, câmera nem identificador de publicidade. Ele só cria um arquivo quando você exporta o histórico em CSV (seção 5).

## 3. Permissões e por que são necessárias

- Dispositivos próximos, buscar (BLUETOOTH_SCAN, Android 12 ou superior): encontrar o BMS. Declarada com "neverForLocation": o escaneamento não é usado para deduzir sua localização.
- Dispositivos próximos, conectar (BLUETOOTH_CONNECT, Android 12 ou superior): conectar ao BMS escolhido.
- Bluetooth e Bluetooth admin (BLUETOOTH, BLUETOOTH_ADMIN), só Android 11 ou inferior: equivalentes antigas das duas anteriores.
- Localização aproximada e precisa (ACCESS_COARSE_LOCATION, ACCESS_FINE_LOCATION), só Android 11 ou inferior: o Android exige essa permissão para escanear Bluetooth nessas versões. O app não lê nem guarda sua localização.
- Serviço em primeiro plano (FOREGROUND_SERVICE, FOREGROUND_SERVICE_CONNECTED_DEVICE): manter a conexão Bluetooth com o BMS enquanto o app está em segundo plano, em dois casos. (1) Por padrão ("Manter sempre conectado" desligado): se uma leitura ao vivo estiver em andamento quando você sai do app, a conexão é mantida por uma carência de cerca de 60 segundos; depois o app fecha a conexão e o serviço para. (2) Com "Manter sempre conectado" ligado: a conexão é mantida até você desligar a opção, tocar em Desconectar na notificação ou tocar em Parar no app.
- Notificações (POST_NOTIFICATIONS): usada só para a notificação desse serviço em primeiro plano. Ela mostra o percentual de carga e a potência e pode aparecer na tela de bloqueio. Se você negar a permissão, a conexão continua, mas sem aviso visível. O app não envia outras notificações; os alertas aparecem só dentro do app.
- Manter ativo (WAKE_LOCK): um wake lock parcial, mantido por no máximo 75 segundos. Cobre os 60 segundos de tolerância em segundo plano, a liberação do enlace Bluetooth e um ciclo de reconexão. É mantido mesmo com "Manter sempre conectado" desligado.

O app usa o recurso de links do Android só para abrir a tela de configurações do sistema para o aplicativo.

## 4. O que fica guardado no seu aparelho

Tudo é guardado localmente, no armazenamento privado do app (AsyncStorage):

- Baterias salvas (até 10), cada uma com um identificador opaco (que pode ser o endereço Bluetooth, nunca exibido) e um apelido que você escolhe; a bateria fixada.
- Idioma, tema (automático, escuro ou claro), limites de alerta e a opção "Manter sempre conectado".
- A última leitura de cada bateria.
- Histórico de leituras por bateria: SOC, tensão, corrente, potência, diferença entre células, tensão mínima e máxima de célula e temperatura máxima. Guardado por minuto e, após 48 horas, agrupado em intervalos de 15 minutos, por até 30 dias, limitado a cerca de 2,5 MB.

O app não criptografa os dados em repouso; eles ficam no armazenamento privado do app no Android. O backup automático do Android (nuvem e transferência entre aparelhos) está desativado para o app.

## 5. Exportação e compartilhamento

- O desenvolvedor não recebe nenhum dado.
- Na tela de Histórico você pode exportar um arquivo CSV pela folha de compartilhamento do Android. Isso só acontece quando você toca em exportar. O app cria um arquivo temporário para o compartilhamento. O arquivo contém horários em UTC e as leituras, sem identificador da bateria, apelido nem endereço Bluetooth.
- O app, por conta própria, não envia o CSV a lugar nenhum. Você escolhe o app de destino e, a partir daí, vale a política de privacidade desse app.
- O app não vende dados nem os compartilha com terceiros por conta própria.

## 6. Retenção e exclusão

- O histórico é mantido por no máximo 30 dias e limitado a cerca de 2,5 MB.
- "Apagar histórico desta bateria" apaga só o histórico daquela bateria.
- O app não tem função para remover uma bateria salva. Para remover baterias salvas, identificadores, apelidos, últimas leituras e configurações, limpe os dados do app nas configurações do Android ou desinstale o app.
- Como os dados ficam só no seu aparelho, o desenvolvedor não tem acesso a eles e não pode atender pedidos de exclusão; a exclusão é feita por você, como acima.
- Um CSV exportado é um arquivo separado, fora do app; apague-o você mesmo no local onde o salvou ou enviou.

## 7. Crianças

O aplicativo não é direcionado a crianças e não trata conscientemente dados de crianças.

## 8. Alterações

Mudanças nesta política serão publicadas nesta página com nova data de vigência.

## 9. Contato

alan.perius.mv@gmail.com

---
