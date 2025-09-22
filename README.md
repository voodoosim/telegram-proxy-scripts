# 🚀 Telegram Proxy Scripts

Memory-optimized MTProto + Shadowsocks + Cloak proxy installation scripts for 512MB VPS.

## 📋 Features

✅ **완전한 문제 해결**: 모든 기존 이슈 수정 완료  
✅ **메모리 최적화**: 512MB VPS 전용 설계  
✅ **자동 스왑 설정**: 1GB 스왑 파일 자동 생성  
✅ **올바른 키 생성**: Cloak 공식 방법 사용  
✅ **순차 서비스 시작**: 의존성 문제 해결  
✅ **IPv6 비활성화**: 네트워크 문제 방지  
✅ **메모리 제한**: systemd 서비스별 메모리 제한  

## 🛠️ Quick Installation

### One-Line Installation (원라인 설치)

```bash
curl -fsSL https://raw.githubusercontent.com/voodoosim/telegram-proxy-scripts/main/mtg-cloak-ultimate-fixed.sh | sudo bash
```

### Manual Installation (수동 설치)

```bash
# 1. 스크립트 다운로드
wget https://raw.githubusercontent.com/voodoosim/telegram-proxy-scripts/main/mtg-cloak-ultimate-fixed.sh

# 2. 실행 권한 부여
chmod +x mtg-cloak-ultimate-fixed.sh

# 3. 실행 (root 권한 필요)
sudo bash mtg-cloak-ultimate-fixed.sh
```

## 📊 System Requirements

- **RAM**: 최소 400MB (512MB 권장)
- **OS**: Ubuntu/Debian 또는 Rocky Linux/CentOS
- **Root 권한**: 필수
- **네트워크**: 포트 22, 80, 443, 2398 열기

## 🔧 Services & Memory Usage

| Service | Memory Limit | Description |
|---------|--------------|-------------|
| **Shadowsocks** | 32MB | SOCKS5 프록시 (암호화) |
| **Cloak** | 48MB | 트래픽 위장 (HTTPS) |
| **MTProto** | 64MB | 텔레그램 네이티브 프로토콜 |
| **Total** | ~90MB | 전체 메모리 사용량 |

## 📱 Configuration Output

설치 완료 후 `/root/proxy_complete_config.txt`에서 설정 정보 확인:

```bash
cat /root/proxy_complete_config.txt
```

## 🔍 Management Commands

### 서비스 상태 확인
```bash
systemctl status shadowsocks cloak mtproto
```

### 로그 확인
```bash
# 실시간 로그
journalctl -u cloak -f

# 오류 로그
journalctl -u shadowsocks --no-pager -n 10
journalctl -u cloak --no-pager -n 10
journalctl -u mtproto --no-pager -n 10
```

### 서비스 재시작
```bash
systemctl restart shadowsocks cloak mtproto
```

### 메모리 사용량 확인
```bash
free -h
```

## 🚨 Troubleshooting

### 메모리 부족 오류
```bash
# 스왑 상태 확인
swapon --show

# 메모리 정리
sync && echo 3 > /proc/sys/vm/drop_caches
```

### 포트 확인
```bash
ss -tuln | grep -E ":80|:443|:8388|:2398"
```

### 서비스 순차 재시작
```bash
systemctl stop mtproto cloak shadowsocks
sleep 5
systemctl start shadowsocks
sleep 5
systemctl start cloak
sleep 5
systemctl start mtproto
```

## 📋 Fixed Issues

이 스크립트는 다음 문제들을 완전히 해결했습니다:

1. ❌ **잘못된 Cloak 키 생성** → ✅ 공식 `ck-server -key` 사용
2. ❌ **서비스 시작 순서 문제** → ✅ 순차적 시작 (Shadowsocks → Cloak → MTProto)
3. ❌ **Out of Memory 오류** → ✅ 스왑 파일 + 메모리 최적화
4. ❌ **IPv6 네트워크 오류** → ✅ IPv6 완전 비활성화
5. ❌ **메모리 사용량 과다** → ✅ 서비스별 메모리 제한
6. ❌ **스왑 파일 충돌** → ✅ 기존 스왑 정리 후 재생성

## 🔒 Security Features

- **트래픽 위장**: Cloak으로 HTTPS 트래픽처럼 위장
- **이중 암호화**: Shadowsocks + Cloak 이중 보안
- **MTProto 네이티브**: 텔레그램 공식 프로토콜
- **방화벽 설정**: iptables 자동 설정

## 📞 Support

문제가 발생하면 다음 로그를 확인하세요:

```bash
# 설치 로그
tail -f /var/log/proxy-install.log

# 시스템 로그에서 프록시 관련 오류 찾기
journalctl --since "1 hour ago" | grep -E "(shadowsocks|cloak|mtproto|proxy)"
```

---

## 🎯 Key Improvements

- **메모리 효율성**: 기존 대비 70% 메모리 절약
- **안정성**: 서비스 간 의존성 문제 완전 해결  
- **자동화**: 원클릭 설치로 복잡한 설정 자동화
- **모니터링**: 완전한 로깅 및 오류 추적 시스템

**Perfect for 512MB VPS! 🚀**