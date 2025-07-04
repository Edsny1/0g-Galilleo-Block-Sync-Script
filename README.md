# 0g-Galilleo-Block-Sync-Script

```
#!/bin/bash

while true; do
  local_height=$(curl -s http://localhost:26657/status | jq -r .result.sync_info.latest_block_height)
  network_height=$(curl -s http://37.27.60.37:26657/status | jq -r .result.sync_info.latest_block_height)

  if [[ -n "$local_height" && -n "$network_height" && "$local_height" =~ ^[0-9]+$ && "$network_height" =~ ^[0-9]+$ ]]; then
    blocks_left=$((network_height - local_height))
    echo "-------------------------------"
    echo "Node height     : $local_height"
    echo "Network height  : $network_height"
    echo "Remaining blocks: $blocks_left"
  else
    echo "Hata: Blok yükseklik bilgileri alınamadı veya geçersiz sayı."
  fi

  sleep 5
done
```
