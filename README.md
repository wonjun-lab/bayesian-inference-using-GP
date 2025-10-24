# Bayesian Inference using Gaussian Process

PyMC를 활용한 Bayesian Model Calibration 및 Gaussian Process 모델링 예제

> Windows 환경 기준으로 작성되었습니다.

## 목차

- [환경 설치](#환경-설치)
- [프로젝트 구조](#프로젝트-구조)
- [예제](#예제)
- [의존성](#의존성)
- [문제 해결](#문제-해결)
- [참고 자료](#참고-자료)

## 환경 설치

### Prerequisites

- Git ([다운로드](https://git-scm.com/download/win))
- uv 설치:
  ```powershell
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```
  또는 winget 사용:
  ```powershell
  winget install --id=astral-sh.uv -e
  ```

### 설치

```bash
# 저장소 클론
git clone https://github.com/wonjun-lab/bayesian-inference-using-GP.git
cd bayesian-inference-using-GP

# Python 및 의존성 자동 설치
uv sync

# Jupyter Notebook 실행
uv run jupyter notebook
```

`uv sync` 명령어는 `.python-version`에 명시된 Python 버전을 자동으로 다운로드하고, 가상환경을 생성하며, 모든 패키지를 설치합니다.

### 가상환경 활성화 (선택사항)

**PowerShell:**
```powershell
.venv\Scripts\Activate.ps1
```

**CMD:**
```cmd
.venv\Scripts\activate.bat
```

## 프로젝트 구조

```
bayesian-inference-using-GP/
├── examples/
│   └── pymc-gp-toy_model.ipynb    # GP 기반 Bayesian Calibration 예제
├── dataset/
│   ├── datacomp_hourly.csv        # 컴퓨터 시뮬레이션 데이터
│   ├── datacomp_monthly.csv
│   ├── datafield_hourly.csv       # 실제 관측 데이터
│   └── datafield_monthly.csv
├── pyproject.toml
├── uv.lock
└── README.md
```

## 예제

### `pymc-gp-toy_model.ipynb`

Kennedy and O'Hagan (2001)의 Bayesian Model Calibration 방법론을 기반으로 한 Gaussian Process 예제입니다.

**주요 내용:**
- 컴퓨터 시뮬레이션 데이터와 실제 관측 데이터 통합
- GP를 에뮬레이터로 활용한 모델 캘리브레이션
- NUTS 샘플러를 통한 파라미터 사후 분포 추정
- 불확실성 정량화 및 예측

**데이터:**
- 시뮬레이션 데이터: 에너지 사용량, 외기온도, 상대습도, 물리적 파라미터 (기기밀도, 조명밀도, COP)
- 관측 데이터: 에너지 사용량, 외기온도, 상대습도

## 의존성

주요 패키지 (모두 `uv sync`로 자동 설치):

- **pymc** (≥5.25.1) - Bayesian 모델링 프레임워크
- **numpyro** (≥0.19.0) - NUTS 샘플러 백엔드
- **jax** (≥0.8.0) - 자동 미분 및 가속
- **numpy**, **matplotlib**, **jupyter**

전체 의존성 목록: `pyproject.toml`

## 문제 해결

**uv 명령어를 찾을 수 없음**
- 터미널 재시작 또는 시스템 재부팅

**PowerShell 실행 정책 오류**
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

**uv sync 실패**
```cmd
rmdir /s .venv
uv sync
```

**Jupyter 실행 불가**
```cmd
uv run jupyter notebook
```

## 참고 자료

- [PyMC Documentation](https://www.pymc.io/)
- [PyMC GP Marginal Implementation](https://www.pymc.io/projects/examples/en/latest/gaussian_processes/GP-Marginal.html)
- [uv Documentation](https://docs.astral.sh/uv/)
- Kennedy, M. C., & O'Hagan, A. (2001). Bayesian calibration of computer models. *Journal of the Royal Statistical Society: Series B*, 63(3), 425-464.

## License

MIT

