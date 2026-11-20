# 유료(광고 없음) 출시 체크리스트

## 1. 앱 코드 (로컬)
- [ ] **라이선스 확인**: 앱·모델이 AGPL/GPL 코드나 가중치(예: Ultralytics YOLOv5/v8/11, AGPL-3.0)를 쓰면 소스 비공개 유료 배포가 불가능 → 상업 라이선스 구매 또는 Apache/MIT 계열 모델로 교체
- [ ] AdMob SDK 제거: `build.gradle`의 `com.google.android.gms:play-services-ads` 의존성, `AndroidManifest.xml`의 `com.google.android.gms.ads.APPLICATION_ID` meta-data, 광고 초기화·배너 코드, UMP 동의(consent) 코드
- [ ] Manifest 최종 권한 확인: AdMob이 끌어오던 `com.google.android.gms.permission.AD_ID`가 남아 있으면 `tools:node="remove"`로 제거
- [ ] 광고가 없으면 `INTERNET` 권한이 필요한지 확인 (분석이 완전히 기기 안에서 끝나면 빼는 것을 권장)
- [ ] 사진 접근은 Photo Picker 사용 (`READ_MEDIA_IMAGES` 권한 없이)
- [ ] targetSdk를 Play의 현재 최소 요구 수준 이상으로 설정
- [ ] `versionCode` / `versionName` 정리, 서명된 릴리스 AAB 빌드 (Play 앱 서명 사용)

## 2. Play Console 설정
- [ ] 결제 프로필(판매자 계정) 생성 및 연결 → 유료 가격 설정 가능해짐
- [ ] **처음부터 "유료" 앱으로 설정** (무료로 출시한 앱은 나중에 유료로 바꿀 수 없음)
- [ ] 가격: USD 0.99 기준, 국가별 자동 환산 확인 (한국 원화 표시가 확인)
- [ ] 판매 국가 선택
- [ ] 앱 콘텐츠
  - [ ] 개인정보처리방침 URL: https://jedobe.github.io/luckylens/privacy/
  - [ ] 광고 포함 여부: **아니요**
  - [ ] 광고 ID 사용: **아니요** (1단계에서 AD_ID 권한 제거한 경우)
  - [ ] 데이터 보안(Data safety): 아래 3번 참고
  - [ ] 콘텐츠 등급 설문 (폭력·사용자 간 상호작용·위치 공유 모두 없음 → 전체이용가 예상)
  - [ ] 타겟층: 만 14세 이상(또는 18세 이상) — 방침의 아동 조항과 맞추기
- [ ] 스토어 등록 정보: `store/listing.md`

## 3. 데이터 보안(Data safety) 답변 초안
- 앱이 사용자 데이터를 수집하거나 공유하나요? → **아니요**
  - 사진은 기기 안에서만 처리되고 전송되지 않으므로 "수집"에 해당하지 않음
  - 결제는 Google Play가 처리하므로 앱의 데이터 수집에 포함하지 않음
- 전송 중 데이터 암호화 / 데이터 삭제 요청 → 수집 데이터가 없으므로 해당 없음

## 4. 테스트 → 출시
- [ ] 비공개 테스트 트랙에 AAB 업로드 (2023-11 이후 생성된 개인 계정: 테스터 12명 이상이 14일 연속 참여해야 프로덕션 신청 가능)
- [ ] 테스터에게도 유료 앱이므로 라이선스 테스터 등록 또는 프로모션 코드 배포 고려
- [ ] 14일 후 프로덕션 액세스 신청 → 심사 → 출시

## 5. 출시 후
- [ ] 랜딩 페이지에 Google Play 링크 추가
- [ ] 앱 소스는 이 공개 저장소에 올리지 않기 (필요하면 별도 private 저장소 사용)
